+++
title = "5.1 - Modify the RDS SG"
weight = 10
+++

The first step in migrating the database component into Amazon RDS is to ensure that traffic coming from the Amazon Lightsail VPC is allowed to reach the RDS service. This is done by adding the IP address range (172.26.0.0/16) of the Amazon Lightsail VPC to the existing Amazon RDS security group.

* Navigate to the <a href="https://us-west-2.console.aws.amazon.com/rds/home?region=us-west-2#databases:" target="_blank">Amazon RDS databases page</a> 

{{% notice tip %}}
The link above redirects to the US West 2 AWS region. Ensure that you're working in the same region where you previously deployed your lab resources. 
{{% /notice %}} 

* From the list of databases, click on the name of the Amazon RDS database you created earlier (the suggested name for this database was ***tasks-db***) to access the database details screen. 
    
    ![](../../images/rds-database-name.jpg?classes=border)

* Scroll down a bit and Under ***Security*** click on the name of the security group for your Amazon RDS database (your security group name will be different than the one listed below)

    ![](../../images/select-rds-sg.jpg?classes=border)

* At the bottom of the screen click on the ***Inbound*** tab to access the rules that define what traffic is allowed to reach the Amazon RDS database. 

    ![](../../images/inbound-tab.jpg?classes=border)

* Click the ***Edit*** button

    ![](../../images/edit-sg-button.jpg?classes=border)

* Click ***Add Rule***

    ![](../../images/add-sg-rule.jpg?classes=border)

* Enter the following values

    * **Type**: MYSQL/Aurora 
    * **Source**: Custom with a CIDR range of 172.26.0.0/16

   ![](../../images/sg-rules.jpg?classes=border)

* Click ***Save*** 

    ![](../../images/save-sg-rule.jpg?classes=border)



