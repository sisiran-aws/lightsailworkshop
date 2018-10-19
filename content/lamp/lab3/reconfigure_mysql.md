+++
title = "3.1 - Reconfigure MySQL"
weight = 10
+++

In this section we'll update the application configuration file (***config.php***) to point to our highly-available Lightsail database. 

* From the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a> select ***Databases*** from the horizontal menu

    ![](../../images/databases-menu.jpg?classes=border)

* Click on the name of the Lightsail database you created earlier

* Under ***Connection details*** make note point of the value for ***Endpoint***.

![](../../images/endpoint.jpg?classes=border)


* Create an environment variable (***LS_ENDPOINT***) to hold the value of your databases endpoint. For example: 

        LS_ENDPOINT='ls-1caf883f5883153cbe5324a8eab2b45eee39d38c.cdekwlh0imih.us-west-2.rds.amazonaws.com'

{{% notice tip %}}
Be sure to use your own value. Do not copy and paste the value above. 
{{% /notice %}}

* Now set environment variables for the default username (***dbmasteruser***) and the password you created earlier (***taskstasks***)

        LS_USERNAME=dbmasteruser && LS_PASSWORD=taskstasks

* Check to make sure the envrionment variables are set correctly:

        echo "Endpoint = "$LS_ENDPOINT && echo "Username = "$LS_USERNAME && echo "Password = "$LS_PASSWORD

* Create a new configuration file that points to the Lightsail database:

        cat /opt/bitnami/apache2/configs/config.php.bak | \
            sed "s/<endpoint>/$LS_ENDPOINT/; \
            s/<username>/$LS_USERNAME/; \
            s/<password>/$LS_PASSWORD/;" \
            >> /opt/bitnami/apache2/configs/config.php.lightsail_db

* Verify the file was modified appropriately

        cat /opt/bitnami/apache2/configs/config.php.lightsail_db

* Activate the new configuration

        cp /opt/bitnami/apache2/configs/config.php.lightsail_db /opt/bitnami/apache2/configs/config.php

* Verify that the active configuration file was modified

        cat /opt/bitnami/apache2/configs/config.php

* Run the ***intall.php*** script to configure the database by visiting `http://<your lightsail instance public IP>/install.php.` (You need to do this again since the front-end is now pointing to a new database)

![](../../images/database-success.jpg?classes=border)

{{% notice tip %}}
If your web app is stil showing the previously deployed database (the one where you created tasks), you may need to use either a new browser window or an incognito window. 
{{% /notice %}}

* Test the new database by visiting `http://<your lightsail instance public IP>/`. Since you have pointed the front-end at a the new database there shouldn't be any tasks to display. 

* Next you will migrate the data out of our local MySQL database and into the Lightsail managed one. This is accomplished by to command line utilities: ***mysqldump*** and ***mysql***. The command below uses ***mysqldump*** to extract the content from the local database and then pipes it to as input the the ***mysql*** command which loads it in the Lightsail managed database

        mysqldump -u root \
        --databases tasks \
        --single-transaction \
        --compress \
        --order-by-primary  \
        -p$(cat /home/bitnami/bitnami_application_password) \
        | mysql -u $LS_USERNAME \
        --port=3306 \
        --host=$LS_ENDPOINT \
        -p$LS_PASSWORD 

{{% notice tip %}}
You will see two warnings regarding supplying a passwoard via the command line. These can safely be ignored, but do note that in production you shouldn't supply passwords via the command line especially in scripts. 
{{% /notice %}}

* Refresh the web page and you should see that the tasks you created originally are now present in the Lightsail managed database. 