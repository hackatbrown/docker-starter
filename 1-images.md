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
