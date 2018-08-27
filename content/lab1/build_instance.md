+++
title = "1.1 - Build the MEAN instance"
weight = 10
+++

The first step in deploying the Todo application is creating a MEAN stack instance in Lightsail. When creating the instance, you will supply a Lightsail launch script to actually install the application.

1) From the Lightsail console click ***Create Instance***

![](../../images/1-1-1.jpg?classes=border)

2) Under ***Blueprint*** choose ***MEAN***
    
![](../../images/1-1-2.jpg?classes=border)

3) Click ***+Add Launch Script***

![](../../images/1-1-3.jpg?classes=border)

4) Paste the script below into the text box

```
#! /bin/bash
sudo /opt/bitnami/ctlscript.sh stop apache
sudo mv /opt/bitnami/apache2/scripts/ctl.sh /opt/bitnami/apache2/scripts/ctl.sh.disabled

cd /home/bitnami
sudo git clone https://github.com/mikegcoleman/todo
cd /home/bitnami/todo
sudo npm install --production

sudo cat << EOF >> /home/bitnami/todo/.env
PORT=80
DB_URL=mongodb://tasks:tasks@localhost:27017/?authMechanism=SCRAM-SHA-1&authSource=tasks
EOF
```

This script does the following:

* Stops Apache using the control scripts present in the Bitnami MEAN image. Stopping Apache frees up Port 80 so the application can use it. 
* Clones the application GitHub repo and installs all the dependencies using the Node Package Manager (***npm***)
* Creates a configuration file that sets the application port (***80***) and the connection string for the database running on the local host (***mongodb://tasks:tasks@localhost:27017/?authMechanism=SCRAM-SHA-1&authSource=tasks***)

5) Name the instance ***MEAN***

![](../../images/1-1-5.jpg?classes=border)

6) Click ***Create***

![](../../images/1-1-6.jpg?classes=border)

Once the instance shows a state of running in the Lightsail console, SSH into it either using the built in SSH client or using your own (username: ***bitnami***). If you are unfamiliar with SSH please see this tutorial. 

![](../../images/mean-running.jpg?classes=border)

{{% notice tip %}} 
Even though the instance shows a state of running, it may still be executing the startup script, and you won't be able to connect. If this is the case, give it a couple of minutes and try again. \
{{% /notice %}}