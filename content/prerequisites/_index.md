---
title: "Using SSH with Lightsail"
weight: 60
---

#### SSH Access

There are two ways to access a Lightsail Linux instance. 

##### Users unfamiliar with SSH
One is using our browser-based SSH client. This method is easy and convenient, but copy and paste operations require an intermediate step. For more information on using SSH via the browser <a href="https://lightsail.aws.amazon.com/ls/docs/en/articles/lightsail-how-to-connect-to-your-instance-virtual-private-server" target="_blank">read this article</a>.

##### Experienced SSH Users

You can access your Lightsail instances using your preferred SSH client such as the built in terminal on a Mac or PUTTY on Windows. In order to do this you will need to download your SSH key from Lightsail. You'll also need to be aware of the username for each instance (for these labs the username is provided in the instructions), as well as the instance IP. 

To use your own SSH client follow these steps:

1) From the Lightsail home page click on ***Account*** and select ***Account***

![](../../images/account.jpg?classes=border)

2) On the horizontal menu select ***SSH Keys***

![](../../images/keys.jpg?classes=border)

3) You will see a list of available keys. Lightsail will create a default key for any region in which you've previously deployed an instance. Choose the key you wish to use and click ***Download*** - *make a note of where the .pem file was downloaded* 

![](../../images/download.jpg?classes=border)

{{% notice tip %}}
The key file will have the extension ***.pem*** and will be named ***LightsailDefaultPrivateKey-region.pem***** - where region is the region from which you downloaded the key. For instance LightsailDefaultPrivateKey-us-east-1.pem.
{{% /notice %}}

{{% notice tip %}}
While default keys may share the same name, they are unique for each Lightsail account. 
{{% /notice %}}

4) Obtain the Public IP address of your lightsail instance. This can be found on the card for the instance on the Lightstail home page. 

![](../../images/mean-ip.jpg?classes=border) 

5) Make sure you know the username for the instance you are accessing. For instance the MEAN and Node.js instances you will be using have the username *bitnami* and the Ubuntu instance you will be using has the username *ubuntu*

6) Issue the SSH command to access the instance. For instance on a Mac or Linux machine the following command would use your default key from us-east-1 region to log into an instance with an IP of 355.355.355.355 (this is not a real IP, of course) with the username *bitnami*

    ssh -i ~/Downloads/LightsailDefaultPrivateKey-us-east-1.pem bitnami@355.355.355.355

{{% notice tip %}}
If you get an error that the permissions are too permissive on your private key, you will need to change them by issuing the following command (substituting in the correct path to your private key)

    chmod 600 ~/Downloads/LightsailDefaultPrivateKey-us-east-1.pem
{{% /notice %}}

{{% notice tip %}}
For Windows users <a href="https://lightsail.aws.amazon.com/ls/docs/en/articles/lightsail-how-to-set-up-putty-to-connect-using-ssh" target="_blank">this doc</a> explains how to to do setup PUTTY to access Lightsail instances
{{% /notice %}}

