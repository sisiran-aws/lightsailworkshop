+++
title = "4.2 - Load balance the front-end"
weight = 35
+++

*  Return to the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a> and choose ***Networking*** from the horizontal menu and click on the name of your previously-created load balancer. 

* Under ***Target instances*** choose ***PHP-fe-1*** from the dropdown list

    ![](../../images/2-4-5.jpg?classes=border)

* Click ***Attach***

    ![](../../images/lamp-attach.jpg?classes=border)

* Click ***Attach another*** 

    ![](../../images/lamp-attach-another.jpg?classes=border)

* Repeat the previous three steps for ***PHP-fe-2*** and ***PHP-fe-3***

{{% notice tip %}}
It will take several minutes for all three instances to register their health checks as ***Passed*** once this has happened, move to the next step
{{% /notice %}}

![](../../images/lamp-passed.jpg?classes=border)

* From the top of the screen copy the long string following ***DNS name:***. This is the URL for your Lightsail load balancer. Any requests on this URL will be routed to one of your three front end instances. 

    ![](../../images/2-4-8.jpg?classes=border)

* Paste the string into a web browser, the Todo application should come up. Reload the page and notice how the host name at the bottom of the screen changes - this indicates that traffic is being routed appropriately. 

