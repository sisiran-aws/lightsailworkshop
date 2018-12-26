+++
title = "1.4 - Deploy the RDS db"
weight = 40
+++ 

Finally, you're going to deploy an Amazon Relational Database Service (RDS) database. Amazon RDS is a hosted database services that offers more advanced features than Lightsail databases (multiple database engines, more instances sizes, read replicas, etc). As your application requirements change, you may find that you need to move from an Amazon Lightsail database to Amazon RDS. Later in this workshop, you'll do just that: migrate your existing Amazon Lightsail database to Amazon RDS. 

* From the <a href="https://us-west-2.console.aws.amazon.com/rds/home?region=us-west-2#GettingStarted:" target="_blank">Amazon RDS getting started page</a> select ***Create database*** from the card on the right. 

    ![](../../images/rds_create_database.jpg?classes=border)

* Under ***Engine options*** choose ***MySQL***

    ![](../../images/mysql_engine.jpg?classes=border)

* Scroll to the bottom of the screen and check the box next to ***Only enable options eligible for RDS Free Usage Tier***

    ![](../../images/rds_free_tier.jpg?classes=border)

* Click ***Next***

    ![](../../images/rds_next.jpg?classes=border)

* Under ***Instance specifications*** set the ***DB engine version*** to ***MySQL 5.7.23*** (this is the same version that you selected for the Amazon Lightsail database)

    ![](../../images/rds_version.jpg?classes=border)

* Scroll to the bottom of the screen, and under ***Setting*** set the following values:

    * **DB instance identifier**: tasks-db
    * **Master username**: dbmasteruser
    * **Master password**: taskstasks

    ![](../../images/rds_settings.jpg?classes=border)

{{% notice tip %}} 
The values for ***Master username*** and ***Master password*** should match the values set for the Amazon Lightsail database earlier. 
{{% /notice %}}

* Click ***Next***

* Under ***Network & Security*** ensure that ***Virtual Private Cloud (VPC)*** is set to your Default VPC. If you do not have a Default VPC, you will need to create one. 

    ![](../../images/default_vpc.jpg?classes=border)

* Scroll to the bottom of the page, and click ***Create database***

{{% notice tip %}}
It will take several minutes for the creation process to complete, so feel free to move on to the next step while this happens. You'll come back to the Amazon RDS database in Lab #5.
{{% /notice %}} 

    