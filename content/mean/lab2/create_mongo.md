+++
title = "2.1 - Deploy MongoDB"
weight = 5
+++

In this section you will deploy a standalone MongoDB instance. To start you will create an Ubuntu Linux instance using an ***OS Only*** blueprint. As part of the instance creation process you'll supply a launch script that will install MongoDB. 

* From the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a> click ***Create Instance***

    ![](../../images/2-1-1.jpg?classes=border)

* Make sure ***Linux/Unix*** is selected under ***Select a platform*** and then under ***Select a blueprint*** click ***OS Only*** and choose ***Ubuntu***

    ![](../../images/2-1-2.jpg?classes=border) 

* Click ***+Add Launch Script***

    ![](../../images/2-1-3.jpg?classes=border) 

* Paste the script below into the text box

        #!/bin/bash
        sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
        echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
        sudo apt-get update
        sudo apt-get install -y mongodb-org

        sudo cat /etc/mongod.conf | sed "s/\b127.0.0.1\b/&,$(hostname -i)/" >> /etc/mongod.conf.new

        sudo mv /etc/mongod.conf /etc/mongd.conf.old
        sudo mv /etc/mongod.conf.new /etc/mongod.conf

        sudo service mongod start

    This script does the following:

    * Uses ***apt-get*** to install Mongo
    * Modifies the Mongo configuration file to make sure Mongo is listening on the instances private IP address
    * Backs up the old configuration file and copies in the new one
    * Starts Mongo

* Scroll down and enter ***Mongo*** as the Instance name

    ![](../../images/2-1-5.jpg?classes=border)

* Click ***Create***

    ![](../../images/2-1-6.jpg?classes=border)

* Once the instance is up and running SSH into the box (username: ***ubuntu***)

* Use the Mongo client to ensure that the machine is running correction

        mongo --host $(hostname -i)

* From the Mongo client to show the built in databases

        show dbs

    The output should be:

        admin   0.000GB
        config  0.000GB
        local   0.000GB

* Type ***exit*** to close the mongo client

* In your web browser from the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console</a> click on the instance name. This will bring up the instance details page

    ![](../../images/2-1-7.jpg?classes=border)

* Document the private IP of the instance. 

    ![](../../images/2-1-8.jpg?classes=border)

{{% notice tip %}}
You will use this IP in the next section
{{% /notice %}}
