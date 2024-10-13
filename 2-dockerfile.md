# Dockerfile

Let's move onto creating our very own images for applications we write!

In order to build a Docker image from an application, we need to copy the contents of that application into something called a Dockerfile. These contents will be various artifacts and dependencies that your application needs.

## What is a Dockerfile?

A Dockerfile is a **blueprint for building Docker images**. It will specify instructions for creating the image environment.

The structure for a Dockerfile will usually follow the same or similar patterns. Let's start with creating an example Dockerfile. The final example Dockerfile can be found in `example-dockerfile-1` in this repository, which you can follow along if you would like!

## Dockerfile Structure

### Base image

Let's take a look at the first line of our Dockerfile that represents a fictitious example Node.js server:

`FROM node`

The first line of the Dockerfile, with the `FROM` keyword, tells us the base image. Whatever image we are building must be based off another image. In this case, `node` is an existing Docker image that we can find on Dockerhub and integrate with our application. Our Docker container in this case will already contain `node` as a dependency.

Often times, we may not want certain dependencies to start with, so we may start with a lower-level image, such as Linux Alpine.

### Environment variables

Next, we can configure environment variables for our Docker image, which we might want if we are running a Node server. Environment variables store information (typically configuration information such as API keys or settings) that are passed to the application at runtime, and allow you to avoid hardcoding environment-specific values in the source code.

```
ENV MONGO_DB_USERNAME=admin \
  MONGO_DB_PWD=password
```

**Note**: You might want to alternatively include these instead externally in something called a `docker-compose` file, which we will go into detail later!

### Running arbitrary commands

Take a look at

`RUN mkdir -p /home/app`

Using the `RUN` Dockerfile keyword, you can run any Linux command. Any commands that you run using this keyword **will only affect the virtualized Docker container, not the host machine!**

Here, we create a directory for our application to live inside `/home/`, called `app/`.

### Copying

Now that we have a directory for our application, we need to get the files in there. With this command:

`COPY ./app /home/app`

we copy the files from our `./app` directory **in our host machine** to the `/home/app` directory on the virtual container.
Unlike `RUN`, `COPY` does in fact execute on the host machine! Otherwise, we wouldn't be able to get our files into the virtual container.

### Setting up our environment

Next up are a few things to help us set up our container environment.

The first is not required, but definitely helps for larger containers. We use the following command:

`WORKDIR /home/app`

to set our current working directory to `/home/app`, where our app lives. This is so that the next commands will execute inside this directory.

Next, we will install the dependencies required by our application using the following command:

`RUN npm install`

You have already seen the `RUN` keyword. We use it here to install the `node` packages directly to the containerized environment.


### Running our application

Lastly, when we run our container, we want our app to run. We use the `CMD` keyword to specify the entrypoint command that is run when the Docker image is run.

`CMD ["node", "server.js"]`

Here, we use the `node` command (which is included through our base image!) to run our `server.js`. Note that even though our app lives in `/home/app/server.js`, we do not need to specifiy this full filepath, because we've set the working directory to `/home/app`!