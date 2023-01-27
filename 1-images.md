# Docker Images

One very important use case of Docker is to **run existing packaged dependencies** for your application in a container. Your application might want to run its own MongoDB or Postgres cluster, or need to communicate with Apache Zookeeper. We can run these dependencies as their own separate Docker containers.

In the upcoming tutorials, we'll cover how to set up a container for your own application. We'll also show you how you can combine and orchestrate multiple containers including both your application containers and the pre-built dependency containers!

## Images and Containers

Docker containers are made up of layers of **images**, which are the files of configuration data necessary to be installed for the container.

For example, a Docker container running Postgres might have these image layers:
- `postgres:10.10` (application image layer)
- [intermediate layers]
- `alpine:3.10` (Linux base image layer)

Notice how the bottommost layer is the layer for the operating system, usually specifying a Linux image. Each successive layer will include more specific dependencies as we move up towards the application image layer.

### Difference between containers and images

You might hear the terms container and image being used frequently with respect to Docker. They, however, are not the same.

A **container** is a _running environment_ for an **image**.

A container will contain its own:
- a virtual filesystem
- environment configurations
- application image

## Prebuilt Official Images

Let's demonstrate an example. Head over to the (official Dockerhub website)[https://hub.docker.com/] and search for Postgres. Then, go to the Docker official image for Postgres. Here, you can see information for Postgres, including different versions and configuration details.

Notice in the top right hand side, there is a command to easily download or pull the Docker image to your machine. If you would like, run this command,

`docker pull postgres`

to pull the latest version of the Postgres image to your machine. You can even specify a specific version if you would like as such

`docker pull postgres:<version number>`.

## Running Images

You can then run your image by executing the command

`docker run postgres`

which will run the Postgres image on your machine. Now, on a different terminal, run the following command:

`docker ps`

to list all current running Docker processes. You should see Postgres in the list. We will go over more use cases of this command, but keep it in mind!

Next, let's move on to creating your own Dockerfile to create am image for your own application!

