+++
title = "5.3 - Reconfigure DB connection"
weight = 30
+++

In this section we'll again update the application configuration file (***config.php***) to point to the RDS database. 

Because our current Lightsail instances are all running under a load balancer, it would be unwise to reconfigure of them to point to the Amazon RDS database. Doing so could result in a situation where the load balancer would present some front-ends connecting to the Lightsail Database, and some connecting to the RDS database. 

To avoid this, you're going to deploy a new PHP front-end instance based on your existing snapshot, and then modify that instance. 

* Navigate to the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/snapshots" target="_blank">Amazon Lightsail snapshots page</a> 

* Click the down arrow on the card for the the ***php-fe-1*** instance to reveal your previously created snapshot. 

![](../../images/snapshot-down-arrow.jpg?classes=border)

* Click the 3 dot menu to the right of the previously created snapshot and select ***Create new instance***

    ![](../../images/three-dots-rds.jpg?classes=border)

    ![](../../images/rds-create-new-instance.jpg?classes=border)

* Scroll down and name the instance ***php-fe-rds***

    ![](../../images/name-php-fe-rds.jpg?classes=border)

* Click ***Create***

Now that you have a new instance to work from, you can reconfigure the configuration file to point to the Amazon RDS database

* Establish an SSH session into your newly created Amazon Lightsail instance (***php-fe-rds***)

* Navigate to the <a href="https://us-west-2.console.aws.amazon.com/rds/home?region=us-west-2#databases:" target="_blank">Amazon RDS databases page</a> 

{{% notice tip %}}
The link above redirects to the US West 2 AWS region. Ensure that you're working in the same region where you previously deployed your lab resources. 
{{% /notice %}} 

* From the list of databases, click on the name of the Amazon RDS database you created earlier (the suggested name for this database was ***tasks-db***) to access the database details screen. 
    
    ![](../../images/rds-database-name.jpg?classes=border)

* Scroll down a bit and from under the ***Endpoint & port*** section copy the value under ***Endpoint***
    
    ![](../../images/rds-endpoint.jpg?classes=border)

* Move back into the SSH session for your ***php-fe-rds*** instance

* Create an environment variable (***RDS_ENDPOINT***) to hold the value of your databases endpoint. For example: 

        RDS_ENDPOINT='tasks-db.workshop.us-west-2.rds.amazonaws.com'

{{% notice tip %}}
Be sure to use your own value. Do not copy and paste the value above. 
{{% /notice %}}

* Now set environment variables for the default username (***dbmasteruser***) and the password you created earlier (***taskstasks***)

        RDS_USERNAME=dbmasteruser && RDS_PASSWORD=taskstasks

* Check to make sure the envrionment variables are set correctly (the output from the command below should match the values you just set for the RDS endpoint, the RDS username, and the RDS password):

        echo "Endpoint = "$RDS_ENDPOINT && echo "Username = "$RDS_USERNAME && echo "Password = "$RDS_PASSWORD


* Create a new configuration file that points to the RDS database:

        cat /opt/bitnami/apache2/configs/config.php.bak | \
            sed "s/<endpoint>/$RDS_ENDPOINT/; \
            s/<username>/$RDS_USERNAME/; \
            s/<password>/$RDS_PASSWORD/;" \
            > /opt/bitnami/apache2/configs/config.php.rds_db

* Activate the new configuration by replacing the existing ***config.php*** with the newly created version that points to the RDS database.

        cp /opt/bitnami/apache2/configs/config.php.rds_db /opt/bitnami/apache2/configs/config.php

* Verify that the active configuration file was modified. The values from the command below should match those of your RDS endpoint, RDS username, and RDS password.

        cat /opt/bitnami/apache2/configs/config.php

* Visit `http://<your php-fe-rds lightsail instance public IP>/install.php.`. You should get the following error: `SQLSTATE[HY000] [1049] Unknown database 'tasks'` This is because while you can reach the Amazon RDS server, the 'tasks' database has no yet been created. 

{{% notice tip %}}
If your web app is stil showing the previously deployed database (the one where you created tasks), you may need to use either a new browser window or an incognito window. 
{{% /notice %}}


In the final step you will migrate the data from your Amazon Lightsail database into your Amazon RDS database. 

This is accomplished by using almost the exact same process you used to migrate from the local MySQL database into your Amazon Lightsail database. 

* From the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a> select ***Databases*** from the horizontal menu

    ![](../../images/databases-menu.jpg?classes=border)

* Click on the name of the Lightsail database you created earlier

* Under ***Connection details*** make note of the value for ***Endpoint***.

![](../../images/endpoint.jpg?classes=border)
* Create an environment variable (***LS_ENDPOINT***) to hold the value of your databases endpoint. For example: 

        LS_ENDPOINT='tasks-db.workshop.us-west-2.LS.amazonaws.com'

{{% notice tip %}}
Be sure to use your own value. Do not copy and paste the value above. 
{{% /notice %}}

* Now set environment variables for the default username (***dbmasteruser***) and the password you created earlier (***taskstasks***)

        LS_USERNAME=dbmasteruser && LS_PASSWORD=taskstasks

* Check to make sure the envrionment variables are set correctly (the output from the command below should match the values you just set for the LS endpoint, the username, and the password):

        echo "Endpoint = "$LS_ENDPOINT && echo "Username = "$LS_USERNAME && echo "Password = "$RDS_PASSWORD

* Issue the following command to export the database into a file (***tasks.sql**)

        mysqldump -u $LS_USERNAME \
        --host $LS_ENDPOINT \
        --databases tasks \
        --single-transaction \
        --compress \
        --order-by-primary  \
        --set-gtid-purged=OFF \
        -p$LS_PASSWORD  > tasks.sql

* Access your RDS instance via the MySQL command line tool

        mysql -u $RDS_USERNAME \
        --port=3306 \
        --host=$RDS_ENDPOINT \
        -p$RDS_PASSWORD 

* Import the previously created database dump file into MySQL

        source tasks.sql;

* Refresh the ***php-fe-rds*** instance web page and you should see that the tasks you created originally are now present in the Amazon RDS managed database. 

From this point you could repeat the steps from Lab 4 and create a new snaphsot from your ***php-fe-rds** instance, deploy to new instances from that new snapshot, and replace the existing instances in your load balancer with your three new RDS-enabled instances. 

This would give you a redundant web front end running in Amazon Lightsail with the database running in Amazon RDS. 

However, for this workshop our last lab will be moving your web front end from Amazon Lightsail to Amazon EC2
