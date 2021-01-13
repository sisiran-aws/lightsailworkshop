+++
title = "Getting started"
weight = 1
+++

### Requirements

In order to get started, you'll need to have **git**, **Docker**, and the **AWS CLI** installed on your machine. Git is included by default on most systems. Docker can be downloaded from [docker.com](https://www.docker.com/). And instuctions to setup the AWS CLI can be found [in the AWS docs](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).

### Get the code

Let's begin by cloning the git repo that contains our source code. Open a terminal window, navigate to the location on your machine where you'd like to store this project, and enter the following command.

```bash
git clone git@github.com:AlexanderRichey/linksaver.git
```
{{% notice tip %}}
The source code of the project is available on GitHub. You can [view it online here](https://github.com/AlexanderRichey/linksaver).
{{% /notice %}}

### Build and run the project

Now let's `cd` into the project and run it.

```bash
cd linksaver
docker-compose up
```
 We're using `docker-compose` here so that we can run multiple containers at the same time. The reason for this is that our application requires a MongoDB database to work.

`docker-compose` is configured in this project with a `docker-compose.yaml` file. This file specifies a MongoDB container and our application container. When we run `docker-compose up`, Docker downloads any container images specified that are not cached locally, builds our application image, and runs them.

In this way, `docker-compose` makes it easy to setup new projects locally. We didn't have to go to the trouble of installing MongoDB locally in order to get this application to work. Nor did we need to install Python, the language in which our application was programmed. With Docker, all of these dependencies are built into the containers themselves and all we have to do is run those containers.

After starting the project with Docker, you should see some logging output not unlike the following.

```log
mongo_1      | 2021-01-12T23:37:10.323+0000 I  NETWORK  [listener] waiting for connections on port 27017
mongo_1      | 2021-01-12T23:37:10.323+0000 I  SHARDING [LogicalSessionCacheReap] Marking collection config.transactions as collection version: <unsharded>
mongo_1      | 2021-01-12T23:37:10.610+0000 I  NETWORK  [listener] connection accepted from 172.19.0.3:47620 #1 (1 connection now open)
mongo_1      | 2021-01-12T23:37:10.610+0000 I  NETWORK  [conn1] received client metadata from 172.19.0.3:47620 conn1: { driver: { name: "PyMongo", version: "3.10.1" }, os: { type: "Linux", name: "Linux", architecture: "x86_64", version: "4.19.121-linuxkit" }, platform: "CPython 3.8.5.final.0" }
mongo_1      | 2021-01-12T23:37:10.612+0000 I  NETWORK  [listener] connection accepted from 172.19.0.3:47622 #2 (2 connections now open)
mongo_1      | 2021-01-12T23:37:10.612+0000 I  NETWORK  [conn2] received client metadata from 172.19.0.3:47622 conn2: { driver: { name: "PyMongo", version: "3.10.1" }, os: { type: "Linux", name: "Linux", architecture: "x86_64", version: "4.19.121-linuxkit" }, platform: "CPython 3.8.5.final.0" }
starlette_1  | INFO:     Started server process [9]
starlette_1  | INFO:     Waiting for application startup.
starlette_1  | INFO:     Application startup complete.
mongo_1      | 2021-01-12T23:37:11.002+0000 I  SHARDING [ftdc] Marking collection local.oplog.rs as collection version: <unsharded>
```

After the logging stops, open a web browser and navigate to `http://localhost:8000`. You should see the following page.

![linksaver screenshot](../../images/linksaver-screenshot.png)

### A note on local development

This project is configured for local development. If you open up one of the source files and make a change, you should see the server restart in the logs. Now let's deploy our project to Lightsail.
