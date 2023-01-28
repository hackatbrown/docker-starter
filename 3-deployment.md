# Deployment

There are a myriad of ways to deploy a Docker container, so we will only give a brief introduction for next steps from here, once you have created your own containerized application.

The brief idea is as follows: once you have a container for your application, you can install run on any machine with Docker installed. This is the beauty of Docker and containerization! This machine could be a virtual machine instance, a real machine in a datacenter you own, etc. Happy deploying!


## Transferring your application files

You will want a way to get your application files and Dockerfile on the machine you are deploying on. You can use something such as FTP or Github to transfer these files to your machine once it is set up.

## Configuring environment variables

If you are deploying a server of sorts that needs to be accessible through the web, you will most likely want to use environment variabes to keep track of things that you want to be configured. This includes things such as the public HTTP port, IP address of your machine etc. While we won't go into it here, this information and more documentation can be found on whatever platform you are deploying on!

## Docker Compose

If you are building a larger application, it is likely that you will have multiple docker containers. And then, on top of that, these containers will often need a way to talk to each other. For example, you might have your server running in a Docker container, and then a MongoDB image running in a Docker container that your server will need to communicate with.

Docker Compose is a way to consolidate all the information that is required for multiple containers to talk to each other in one configuration file. Docker Compose is actually run on the command line as a separate command (i.e. `docker-compose ...`) but it is generally installed with Docker, so if you have installed Docker already, you should be able to run this command without having to do anything extra. If not, you can reference the installation guidelines [here](https://docs.docker.com/compose/install/).

To use Docker Compose, you will want to create a `.yaml` file with the configuration for your container orchestration setup. Docker Compose is enough an entirely different tutorial on its own, so we will only introduce it here. You can get started with the official documentation [here](https://docs.docker.com/compose/), but there are also tons of tutorials online you can follow as well, such as [this tutorial](https://www.baeldung.com/ops/docker-compose) written by Andrea Ligios.


## Example: Deploying on AWS

One example of an accessible deployment method is through AWS. Fortunately, we have [an AWS starter kit for you](https://docs.google.com/document/d/1XzteamYwFEGRTGTG8m8biIxA0nPVrh-IvYqymYOVnQ4/edit)! More information about the specific AWS resources can be found in the starter kit, but we recommend deployment on something like EC2 or Fargate.

The general idea is still the same; you will want to get your application files and Dockerfile on the virtual machine, and then run the Docker image with the right configurations on the machine.