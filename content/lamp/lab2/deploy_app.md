+++
title = "2.1 - Deploy the Application"
weight = 15
+++

In this section we are going to deploy the application code into our lightsail instance, as well as configure the connection between the PHP applicaiton and the locally-running MySQL database.

{{% notice tip %}} 
The following steps are performed from the LAMP instance command line using either your own SSH client or Lightsail's web-based SSH access. 
{{% /notice %}}

* Ensure you are SSH'd into your ***LAMP*** instance, 

* The LAMP Bitnami image has some default web pages installed, you will need to remove those so you can deploy the PHP application. 

        cd /opt/bitnami/apache2/htdocs && rm -rf *

* Use git to clone the appication code onto the server

        git clone https://github.com/mikegcoleman/todo-php .

* The PHP application uses a file (***config.php***) to hold the information necessary to connect to the database (database host name, username, and password). You will need to create a directory to house our configuration files and make the bitnami user the owner. 

        sudo mkdir /opt/bitnami/apache2/configs && \
        sudo chown bitnami:bitnami /opt/bitnami/apache2/configs

{{% notice tip %}}
As a best practice never store sensitive information in the document root of your web server. Ideally, in production you would use a secrets management solution such as AWS Secrets Manager.
{{% /notice %}} 

* Move the config file into the configuaration directory

        sudo mv /opt/bitnami/apache2/htdocs/config.php /opt/bitnami/apache2/configs/config.php

* Export environment variables to aid in editing the configuration file. Note that the default password for the instance database is stored in a file in the home directory (/home/bitnami/bitnami_application_password). 

        ENDPOINT=localhost && \
        USERNAME=root && \
        PASSWORD=$(cat /home/bitnami/bitnami_application_password)

* Verify the environment variables

        echo "Endpoint = "$ENDPOINT && echo "Username = "$USERNAME && echo "Password = "$PASSWORD

* Backup the original config file

        cp /opt/bitnami/apache2/configs/config.php /opt/bitnami/apache2/configs/config.php.bak

* Create a new condfiguration file to work with the locally installed database. The command below uses ***sed*** to go through the configuration file and replace placeholder values with the values of the environment variables you set in the previous step. It writes these values into a new file (***config.php.monolithic***)

        cat /opt/bitnami/apache2/configs/config.php | \
        sed "s/<endpoint>/$ENDPOINT/; \
        s/<username>/$USERNAME/; \
        s/<password>/$PASSWORD/;" \
        >> /opt/bitnami/apache2/configs/config.php.monolithic

* Verify the the monolithic config file is correct by making sure the values in the config file match the values of the environment variables. 

        cat /opt/bitnami/apache2/configs/config.php.monolithic

* Put the new config file into production

        cp /opt/bitnami/apache2/configs/config.php.monolithic /opt/bitnami/apache2/configs/config.php

* Verify that the correct config file is in use in production by making sure the values displayed for the productiong configuration file (***config.php***) match the values of the monolithic file.

        cat /opt/bitnami/apache2/configs/config.php

With the configuration file updated, your PHP application now knows how to connect to the local database. 

* In a real-world application you would have defined processes on how to ready the database for production. In the case of the demo app you need to run a PHP script by pointing your web browser to `http://<your lightsail instance public ip>/install.php`. 

![](../../images/database-success.jpg?classes=border)

{{% notice tip %}}
To find the public IP of your lightsail intance check the card for your instance on the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a>. 
{{% /notice %}}

![](../../images/lamp-ip.jpg?classes=border)

* To see the running application point your web browser to `http://<lightsail instance public IP>/`

* Use the ***Add Task*** button to add a few tasks. 

![](../../images/add-task.jpg?classes=border)

