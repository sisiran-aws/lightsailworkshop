+++
title = "1.2 - Deploy the database"
weight = 20
+++

In this section we'll deploy a Lightsail database. Lightsail databases are a managed database service that allow you to get away from the complexity of deploying and managing database software. Lightsail manages the underlying infrastructure and database engine, you only need to worry about creating and deploying the actual databases and tables running inside the service. 

* From the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a> select ***Databases*** from the horizontal menu

    ![](../../images/databases-menu.jpg?classes=border)

* Click ***Create database***

    ![](../../images/create-database.jpg?classes=border)

{{% notice tip %}}
Make sure you're deploying your database into the same region that you deployed your LAMP instance.
{{% /notice %}}

* Leave the default value for the MySQL version. Additionally, let Lightsail manage the creation of the database credentials. 

* Since the pont of this lab is to deploy a fault-tolerant and scalable implementation of the web application, scroll down and select ***High Availability*** under ***Choose your database plan***.

    ![](../../images/ha.jpg?classes=border)

* Name your database ***todo-db***

    ![](../../images/name-db.jpg?classes=border)

* Click ***Create database*** 

    ![](../../images/create-db.jpg?classes=border)

{{% notice tip %}}
It will take several minutes for the creation process to complete, so feel free to move on to the next step while this happens. You'll come back to the Lightsail database in Lab #3.
{{% /notice %}}   