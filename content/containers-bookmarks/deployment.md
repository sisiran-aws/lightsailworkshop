+++
title = "Deployment"
weight = 3
+++

Since our bookmarking app is dependent on MongoDB, we'll need to setup a MongoDB instance. Next, we'll build and deploy our app to Lightsail Containers.

### MongoDB

We're going to use Lightsail Instances to setup a MongoDB instance that our containerized bookmarking app will connect to once deployed. In Lightsail, setting up MongoDB is fairly easy to do using Lightsail Instances' launch script feature.

1. Navigate to [Lightsail](https://lightsail.aws.amazon.com/) and sign in if you haven't already.
2. On the Instances tab, choose _Create Instance_.
3. Under _Select a blueprint_, choose _OS only_, and then choose _Ubuntu 20.04 LTS_.
4. Under the _Optional_ section, choose _Add launch script_ and paste [the contents of `mongo-cloud-init.sh`](https://github.com/AlexanderRichey/linksaver/blob/master/mongo-cloud-init.sh).

{{% notice warning %}}
The `mongo-cloud-init.sh` script works fine for the purpse of this demo, but it is __not secure for use in production__. Do not use this script for anything other than this demo.
{{% /notice %}}

5. Choose you instance plan—any instance plan should be fine.
6. Name your instance.
7. Finally, choose _Create instance_.
8. After the instance is ready, SSH into it using either Lightsail's webssh feature or through an SSH client.
9. In the instance, run `systemctl status mongod` to make sure MongoDB was installed successfully.
10. **Important:** Note the _internal IP_ of your instance.

### Create a container service

Let's create a container service onto which we'll deploy our containerized bookmarking app.

1. Navigate to [Lightsail](https://lightsail.aws.amazon.com/).
2. Choose the _Containers_ tab.
3. Choose _Create container service_.
4. Complete the form. Skip the _Setup your first deployment section_. Any options should be fine.
5. Choose _Create container service_.

### Build and upload the container image

While the container service is spinning up, let's build and upload our container image.

First, let's install `lightsailctl`, a plugin for the AWS CLI that makes uploading images to Lightsail easier. For Mac and Linux based machines, these commands should install the plugin. For Windows, see the [docs on Lightsail](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-install-software).

```bash
curl "https://s3.us-west-2.amazonaws.com/lightsailctl/latest/darwin-amd64/lightsailctl" -o "/usr/local/bin/lightsailctl"
chmod +x /usr/local/bin/lightsailctl
xattr -c /usr/local/bin/lightsailctl
```

Now `cd` into the `linksaver` project that we cloned earlier and build the application image with the following command.

```bash
docker build . -t linksaver
```

Note that we are tagging the image with the name `linksaver`. This makes it easier for us the upload the image.

```bash
aws lightsail push-container-image --image linksaver \
  --service-name <the service name you gave> \
  --label linksaver
```

Note the image name after the upload succeeds.

### Create deployment

Now we're ready to deploy.

1. Navigate to [Lightsail](https://lightsail.aws.amazon.com/) and choose the container service you created earlier.
2. Choose _Create your first deployment_.
3. Add the following values to the deployment:
    - Container name: `linksaver`
    - Image: `<your service name>.linksaver.1`
    - Leave the launch command empty
    - Add an envrionment variable whose key is `DB_CONNECTION` and whose value is `mongodb://admin:admin@<private ip of your mongo instance>:27017/?authSource=admin`
    - Open port `8000` with protocol `HTTP`
    - Under _Public endpoint_, choose _linksaver_ from the dropdown menu.
4. Choose _Save and deploy_.

Your deployment should look something like this:

![bookmarks contianer deployment](../../images/linksaver-deployment-spec.png?classes=border)

And your _Public endpoint_ settings should look like this:

![bookmarks public endpoint setting](../../images/linksaver-public-endpoint.png?classes=border)

After the deployment completes, navigate to the public url of your container service, found at the top of the container service management page. You should see a page like this:

![linksaver on lightsail](../../images/linksaver-on-ls.png)

{{% notice tip %}}
You can deploy your container to Lightsail from the CLI by running `aws lightsail create-container-service-deployment`. For more information, run `aws lightsail create-container-service-deployment help`.
{{% /notice %}}

