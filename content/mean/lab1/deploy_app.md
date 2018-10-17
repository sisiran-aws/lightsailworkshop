+++
title = "1.3 - Start and test the app"
weight = 25
+++

### 1.3 - Start and test our application

Now that the application is installed and the database configured it is ready to be started. 

{{% notice tip %}}
The following steps are performed from the MEAN instance command line using either your own SSH client or Lightsail's web-based SSH access. 
{{% /notice %}}

* Change into the application directory

        cd ~/todo

* Start the application by executing the following command
    
        sudo DEBUG=app:* ./bin/www

    You should see a message such as:

        app:* Listening on port 80 +0ms

* From the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a> get the IP address of the MEAN instance and navigate to that address in a web browser.

    ![](../../images/mean-ip.jpg?classes=border)

You should see the Todo application running. Add a task or two to make sure it's working as expected.  You can also see the host that is serving up the web front-end (this will become more important in the next section).


![](../../images/2-3-13.jpg?classes=border)

{{% notice tip %}}
You can also check the output in your SSH session to verify everything is working
{{% /notice %}}