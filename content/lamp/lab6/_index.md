+++
title = "LAMP Lab #6 Overview"
weight = 90
+++

### Upgrading to EC2

In the previous section you worked through how to migrate an Amazon Lightsail database to Amazon RDS. In this final lab you'll upgrade your Amazon Lightsail instance to Amazon EC2. 



To do this you will need to:

* Create a snapshot of your RDS-enabled web front-end instance
* Export that snapshot to Amazon EC2
* Create a new Amazon EC2 instance from exported snapshot
* Update the Amazon RDS security group to include the security group for your Amazon EC2 instance

When you're finished you'll have moved the todo application from Lightsail to AWS taking advantage of the full set of functionality within Amazon EC2 and Amazon RDS. 

![](../../images/lamp-architecture-5.jpg?classes=border)