+++
title = "1.3 - Start and test the app"
weight = 25
+++

### 1.3 - Start and test our application

Now that the application is installed and the database configured it is ready to be started. 

{{% notice tip %}}
The following steps are performed from the Lightsail instance command line
{{% /notice %}}

1) Change into the application directory

    cd ~/todo

2) Start the application by executing the following command
    
    sudo DEBUG=app:* ./bin/www

You should see a message such as:

    app:* Listening on port 80 +0ms

3) From the home page of the Lightsail console get the IP address of the MEAN instance and navigate to that address in a web browser.

![](../../images/mean-ip.jpg?classes=border)

{{% notice tip %}}
If you are not on the Lightsail home page click ***Home*** in the upper left corner of the Lightsail console
{{% /notice %}}

You should see the ToDo application running. Add a task or two to make sure it's working as expected. 

{{% notice tip %}}
You can also check the output in your SSH session to verify everything is working
{{% /notice %}}