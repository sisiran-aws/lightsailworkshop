+++
title = "5.2 - Enable VPC peering"
weight = 20
+++

The next step is to ensure that the Lightsail VPC can communicate with your default AWS VPC. By default services in AWS cannot access services running in Amazon Lightsail (and vice versa). However, this can be addressed by using a feature called VPC peering. VPC peering makes it possible for certain AWS services to communicate with Amazon Lightsail resources (in this case the Amazon RDS database will be communicating with the web front end running on an Amazon Lightsail instance).

* Navigate to the <a href="https://lightsail.aws.amazon.com/ls/webapp/account/profile" target="_blank">Amazon Lightsail account settings page</a> 

* From the horizontal menu click ***Advanced***

    ![](../../images/vpc-peering-advanced.jpg?classes=border)

* Scroll down and check the box next to ***Enable VPC peering*** for the region in which you deployed your Lightsail resources (you will only see options for regions that currently have deployed resources)

![](../../images/enable-vpc-peering.jpg?classes=border)