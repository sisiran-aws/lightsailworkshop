+++
title = "3.1 - Reconfigure MySQL"
weight = 10
+++

In this section we'll update the application configuration file (***config.php***) to point to our highly-available Lightsail database. 

* From the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a> select ***Databases*** from the horizontal menu

    ![](../../images/databases-menu.jpg?classes=border)

* Click on the name of the Lightsail database you created earlier

* Under ***Connection details*** click ***show** to display the password Lightsail created when the database was deployed.

![](../../images/show-password.jpg?classes=border)


* Export nvironment Variables using the values from your Lightrsail Database intance. In the case of the image below the variables would be configured as follows. 

{{% notice tip %}}
Be sure to enclose the password in single quotes as it could contain special characters that could cause the copy / paste to fail.
{{% /notice %}}

        ENDPOINT=ls-1caf883f5883153cbe5324a8eab2b45eee39d38c.cdekwlh0imih.us-west-2.rds.amazonaws.com
        USERNAME=dbmasteruser
        PASSWORD='#TEW3(XG1^7A`ff+8Lb3[Zvt9hx>[_l.'

{{% notice tip %}}
Be sure to use your own values. Do not copy and paste the values above. 
{{% /notice %}}

![](../../images/db-details.jpg?classes=border)

* Check to make sure the envrionment variables are set correctly:

        echo "Endpoint = "$ENDPOINT && echo "Username = "$USERNAME && echo "Password = "$PASSWORD

* Create a new configuration file that points to the Lightsail database:

        cat /opt/bitnami/apache2/configs/config.php.bak | \
            sed "s/<endpoint>/$ENDPOINT/; \
            s/<username>/$USERNAME/; \
            s/<password>/$PASSWORD/;" \
            >> /opt/bitnami/apache2/configs/config.php.lightsail_db

* Verify the file was modified appropriately

        cat /opt/bitnami/apache2/configs/config.php.lightsail_db

* Activate the new configuration

        cp /opt/bitnami/apache2/configs/config.php.lightsail_db /opt/bitnami/apache2/configs/config.php

* Verify that the active configuration file was modified

        cat /opt/bitnami/apache2/configs/config.php

* Run a php script to configure the database by visiting `http://<your lightsail instance public IP>/install.php.` (we need to do this again since we're now pointing to a new database)

![](../../images/database-success.jpg?classes=border)

{{% notice tip %}}
If your web app is stil showing the previously deployed database (the one where you created tasks, you may need to use either a new browser window or an incognito window. 
{{% /notice %}}

* Test the new database by visiting `http://<your lightsail instance public IP>/`. Since you have pointed the front-end at a new databse there shouldn't be any tasks to display. 

{{% notice tip %}}
A next logical step here would be to migrate the data from your local database into your lightsail database. However, due to time contraints that exercise is not part of this workshop. If you like to learn more about how to do that, <a href="https://lightsail.aws.amazon.com/ls/docs/en/articles/amazon-lightsail-importing-data-into-your-database" target="_blank">read the Lightsail docs</a>.
{{% /notice %}}