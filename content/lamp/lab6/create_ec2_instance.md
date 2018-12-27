+++
title = "6.2 - Create EC2 Instance"
weight = 35
+++

When the gears stop spinning on the top of the Amazon Lightsail home page, you can move on to the final step of deploying the actual EC2 instance. 

* Return to the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a>

* Click the gear at the top of the page, and select ***Open the Amazon EC2 console***. This will launce the EC2 console to the AMI's page with your newly created AMI selected. 

    ![](../../images/open-ec2-console.jpg?classes=border)

* Click the ***Launch*** button near the top of the screen

    ![](../../images/ec2-launch.jpg?classes=border)

* From the bottom of the next screen click ***Next: Configure Instance Details***

    ![](../../images/configure-instance-details.jpg?classes=border)

* Ensure the new instance is being created in the default VPC

    ![](../../images/default-vpc.jpg?classes=border)

* Click ***Next: Add Storage*** at the bottom of the screen

    ![](../../images/add-storage.jpg?classes=border)

* Click ***Next: Add Tags*** at the bottom of the screen

    ![](../../images/add-tags.jpg?classes=border)

* The web front end needs to be accessible from the internet, so you will need to open incoming access for HTTP (port 80) in the security group. Click ***Next: Configure Security Group*** at the bottom of the screen

    ![](../../images/configure-security-group.jpg?classes=border)

* Provide values for the security group name and description

    ![](../../images/security-group-name.jpg?classes=border)

* Click ***Add Rule***

    ![](../../images/add-rule.jpg?classes=border)

* For ***Type*** choose ***HTTP*** from the drop down. Leave the rest of the values at their defaults

    ![](../../images/security-group-type.jpg?classes=border)

* From the bottom of the screen click ***Review and Launch***

    ![](../../images/review-and-launch.jpg?classes=border)

* From the bottom of the screen click ***Launch***

    ![](../../images/launch.jpg?classes=border)

* On the key pair screen you can either create a new key pair or use an existing one. You don't need to SSH into the instance for this lab, so it doesn't matter which one you pick, but if you don't have an existing key pair you must create a new one. 

* Ensure that you check the box acknowledging that you have access to your key pair, and click ***Launch Instance***

* On the next screen click on your instance ID to bring up the EC2 console with your instance selected. 

    ![](../../images/instance-id.jpg?classes=border)

* Make a note of the IP address under ***IPv4 Public IP*** (you may need to scroll to the right to see the IP address) you will need this at the end of the next section

    ![](../../images/ec2-ip.jpg?classes=border)

* When ***Instance State*** reads ***running*** and ***Status Checks*** reads ***2/2 checks passed*** move on to the next step

    ![](../../images/status-checks.jpg?classes=border)











    