+++
title = "6.1 - Export the LS Snapshot"
weight = 25
+++

The first step in upgrading your Amazon Lightsail instance to an Amazon EC2 instance is to create a new snapshot, then export that snapshot to Amazon EC2.

* Return to the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a>

* Click the 3 dot menu for the ***php-fe-RDS*** instance and choose ***Manage***

    ![](../../images/rds-instance-three-dots.jpg?classes=border)

* From the horizontal menu choose ***Snapshots***

    ![](../../images/2-3-3.jpg?classes=border)

* Click ***Create snapshot***

    ![](../../images/rds-create-snapshot.jpg?classes=border)

{{% notice tip %}}
Under ***Recent snapshots*** the status will change to ***creating***, you will need to wait for the process to complete before moving forward. This can take up to 5 minutes. 
{{% /notice %}}

* Click the 3 dot menu to the right of the newly created snapshot and select ***Export to Amazon EC2***. This will start an operation that will create a new Amazon machine image (AMI) based on the Amazon Lightsail snapshot. The new AMI will be created in the same region as the existing Lightsail snapshot. 

    ![](../../images/rds-recent-snapshots.jpg?classes=border)

* At the first pop-up dialog click ***Yes, continue***

* At the next pop-up dialog click ***Acknowledged***

* You will see a gear start spinning at the top of the Amazon Lightsail homepage. If you click on the gear you'll see the current status of the export operation. 

    ![](../../images/gears.jpg?classes=border)

{{% notice tip %}}
After several minutes the gears will stop spinning, and you can move on to the next exercise. 
{{% /notice %}}