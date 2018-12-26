+++
title = "LAMP Lab #3 Overview"
weight = 80
+++

### Connecting to the Lightsail Database

The first iteration of the application's web front end is not inherently scalable because the database and front end are located on the same machine. It would be problematic to add additional database instances whenever additional front-end capacity was needed. 

To fix this issue the front end and database need to be separated. In this part of this lab you will adjust the configuration for the PHP front-end to point to the previously deployed Lightsail Database. 

![](../../images/lamp-architecture-2.jpg?classes=border)

