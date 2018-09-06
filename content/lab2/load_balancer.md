+++
title = "2.4 - Load balance the front-end"
weight = 35
+++

* Return to the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a> and choose ***Networking*** from the horizontal menu. 

    ![](../../images/2-4-1.jpg?classes=border)

* Click ***Create Load Balancer***

    ![](../../images/2-4-2.jpg?classes=border)

* Scroll down and enter ***todo-lb*** for the load balancer name

    ![](../../images/2-4-3.jpg?classes=border)

* Click ***Create Load Balancer***

    ![](../../images/2-4-4.jpg?classes=border)

* Under ***Target instances*** choose ***node-fe-1*** from the dropdown list

    ![](../../images/2-4-5.jpg?classes=border)

* Click ***Attach***

    ![](../../images/2-4-6.jpg?classes=border)

* Click ***Attach another*** and repeat the previous two steps for ***node-fe-2*** and ***node-fe-3***

    ![](../../images/2-4-7.jpg?classes=border)

{{% notice tip %}}
It will take several minutes for all three instances to register their health checks as ***Passed*** once this has happened, move to the next step
{{% /notice %}}

![](../../images/2-4-7a.jpg?classes=border)

* From the top of the screen copy the long string following ***DNS name:***. This is the URL for your Lightsail load balancer. Any requests on this URL will be routed to one of your three front end instances. 

    ![](../../images/2-4-8.jpg?classes=border)

* Paste the string into a web browser, the Todo application should come up. Reload the page and notice how the host name at the bottom of the screen changes - this indicates that traffic is being routed appropriately. 

