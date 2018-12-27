+++
title = "6.3 - Update RDS SG"
weight = 45
+++

The final step in configuring the new Amazon EC2 intstance to access the Amazon RDS database is to add the instance security group to the RDS security group. This process is very similar to what you did earlier when you added the Amazon Lightysail IP address range to the RDS security group. 

* If you are not still there, go back to the details page for you Amazon EC2 instance and ensure you new instance is selected. 

* Scroll down to the bottom part of the screen where the instance details are listed.

* Click on the security group name

    ![](../../images/click-sg-name.jpg?classes=border)

* Scroll down to the bottom part of the screen where the security group details are listed.

* Make a note of the ***Group ID*** (you can click the copy icon next to the name to copy the ID to your clipboard)

    ![](../../images/group-id.jpg?classes=border)

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
    * **Source**: Paste in the value of your EC2 instace security group you noted above

   ![](../../images/updated-sg-rules.jpg?classes=border)

* Click ***Save*** 

    ![](../../images/save-updated-sg-rule.jpg?classes=border)

* Navigate to the IP address of your Amazon EC2 instance and you should see the todo application up and running. 