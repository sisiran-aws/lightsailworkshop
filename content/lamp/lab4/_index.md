+++
title = "LAMP Lab #4 Overview"
weight = 80
+++

### Scaling the PHP front-end

Now that we have the front-end and database separated, let's take a look at how we can add some scalability and fault tolerance to the web tier. 

In this final section you will take a snapshot of the web front-end, and deploy two additional web web tier instances from that snapshot. Finally, you'll add a load balancer in front of the three front end instances.

When this is all done you'll have a scaled out and fault tolerant version of a sample two-tier web app. 

![](../../images/lamp-architecture-3.jpg?classes=border)