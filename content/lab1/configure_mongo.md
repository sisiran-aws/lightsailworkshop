+++
title = "1.2 - Configure MongoDB"
weight = 15
+++

In this section you are going to configure the Mongo database for use with the application. Specifically you are going to add a username and password  (***tasks*** for both) for the application database (also called ***tasks***). You'll do all this using the Mongo client from the Lightsail command line. 

{{% notice tip %}} 
The following steps are performed from the Lightsail instance command line
{{% /notice %}}

1) Ensure you are SSH'd into your ***MEAN*** instance, and then log into the mongo client using the following command

    mongo admin --username root -p $(cat ./bitnami_application_password)

{{% notice tip %}}
Each Bitnami-based Lightsail instance stores the application password in a file called ***bitnami_application_password***. Below we are redirecting that file into the Mongo client command line.
{{% /notice %}}

2) Create the tasks database by issuing the following command:

    use tasks

3) Add a db admin user to our tasks database by pasting in the lines below into the Mongo client and hitting ***enter***

    db.createUser(
        {
            user: "tasks",
            pwd: "tasks",
            roles: [ "dbOwner" ]
        }
    )

You should get a message that you successfully added the user:

    Successfully added user: { "user" : "tasks", "roles" : [ "dbOwner" ] }

4) Close the mongo shell by typing exit

    exit