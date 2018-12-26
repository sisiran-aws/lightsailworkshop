+++
title = "LAMP Lab #5 Overview"
weight = 80
+++

### Migrating to RDS

At some point your application needs may require features not found in Amazon Lightsail. Fortunately it is straightforward to move one or all of the  parts of your application into other AWS services. 

In this lab you're going to migrate the database component from 
Amazon Lightsail over to Amazon RDS. 

To do this you will need to:

* Add the IP address range (CIDR range) of the Amazon Lightsail VPC to your Amazon RDS security group
* Enable VPC Peering in Amazon Lightsail
* Migrate your data from your Amazon Lightsail database to your Amazon RDS database

This will leave you with an architecture where the front-end is running on an Amazon Lightsail, but the database is now managed by Amazon RDS.

![](../../images/lamp-architecture-4.jpg?classes=border)