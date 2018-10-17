+++
title = "2.2 - Deploy the front-end"
weight = 15
+++

Next you are going to create the web front end instance. To build the front end instance you will start with the Lightsail Node.js blueprint and add in the application code from GitHub. Additionally the isntance will use a process manager, PM2, to ensure that our application starts up automatically.

Check out the [website](http://pm2.keymetrics.io/) to learn more about PM2. 

* From the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a> click ***Create Instance***

    ![](../../images/2-2-1.jpg?classes=border)

* Make sure ***Linux/Unix*** is selected under ***Select a platform*** and then under ***Select a blueprint*** choose ***Node.js***

    ![](../../images/2-2-2.jpg?classes=border)

* Click ***+Add launch script***

    ![](../../images/2-2-3.jpg?classes=border)

* Paste in the script below

        #!/bin/bash

        sudo /opt/bitnami/ctlscript.sh stop apache
        sudo mv /opt/bitnami/apache2/scripts/ctl.sh /opt/bitnami/apache2/scripts/ctl.sh.disabled

        cd /home/bitnami

        sudo git clone https://github.com/mikegcoleman/todo

        cd /home/bitnami/todo

        sudo npm install --production
        sudo npm install pm2@latest -g
        

    This script does the following:

    * Disables Apache to free up port 80 for the web front end
    * Clones in the application code from the GitHub repo
    * Uses ***npm*** to install the application dependencies and PM2
    

* Name the instance ***node-fe-1***

    ![](../../images/2-2-5.jpg?classes=border)

* Click ***Create***

    ![](../../images/2-2-6.jpg?classes=border)

* Wait for the instance to reach a running state, and then SSH into the instance (username: ***bitnami***)

{{% notice tip %}}
The following commands need to be run from the command line of the Node.js instance*
{{% /notice %}}

* Set an environment variable to hold the MongoDB private IP address by executing the command below and substituting the IP address your recorded above.

        IP=<MongoDB instance private IP>

    For example:

        IP=172.12.14.1

* Ensure the IP is correctly set by typing the command below. The output should be the private IP of the MongoDB instance

        echo $IP

* Change into the application directory

        cd ~/todo

* Create a config file to hold our environment variables by pasting the following lines at the command prompt in the NodeJS instance. 

        sudo sh -c "cat > ./.env"  << EOF
        PORT=80
        DB_URL=mongodb://$IP:27017/
        EOF

    These variables specify the port the application will run on, and the connection string for the MongoDB host

* Ensure the file was created succesfully by using ***cat*** to list out the contents

        cat ./.env

    The output should be similar to below (ensure the IP address matches the **PRIVATE IP** of your Mongo instance)

        PORT=80
        DB_URL=mongodb://IP=172.12.14.1:27017/
        
* Configure PM2 for use with Ubuntu by issuing the following command
        
        sudo pm2 startup ubuntu

* Start the application using PM2

        sudo pm2 start /home/bitnami/todo/bin/www

* Save out the current process list for PM2. This will allow PM2 to start the application when the instance boots up subsequently

        sudo pm2 save

* Issue the following command to have PM2 stream the application logs to the console

        sudo pm2 logs www

* Ensure everything is working by navigating the the **PUBLIC IP** of your ***node-fe-1*** Instance

    You should see the todo application in your web browser and if you check the SSH session there should be some output there as well similar to the below:

        0|www  | GET / 200 1005 - 42.341 ms
        0|www  | GET /stylesheets/style.css 200 89 - 2.430 ms
        0|www  | GET /css/bootstrap.min.css 200 140936 - 3.865 ms
        0|www  | GET /css/fontawesome-all.css 200 51609 - 0.807 ms
        0|www  | GET /js/bootstrap.min.js 200 51039 - 4.965 ms
        0|www  | GET /js/jquery.min.js 200 86927 - 2.875 ms

{{% notice tip %}}
You can find the public IP on the card with the instance name for the ***node-fe-1*** instance on the Lightsail home page
{{% /notice %}}

![](../../images/2-2-13.jpg?classes=border)


