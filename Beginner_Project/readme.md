### Building your first Docker image with Jenkins 2

![](https://collabnix.com/wp-content/uploads/2018/03/ci-cd.png)

Containerising your application is like shoving your app and all its dependencies into a box. Except the box is infinitely replicable. Whatever happens in the box, stays in the box - unless you explicitly take something out or put something in. And when it breaks, you’ll just throw it away and get a new one.

**Containers** make your app easy to run on different computers - ideally, the same image should be used to run containers in every environment stage from development to production.

This project is your guide for building a Docker image, and then setting up Jenkins 2 to build and publish the image automatically, whenever you commit changes to your code repository.

###  Requirements

To run through this guide, you will need the following:

**1**. To build and run the Docker image locally: Mac OS X or Linux, and Docker installed.

**2**. To set up Jenkins to build the image automatically: Access to a Jenkins 2.x installation.

### Our application

For this guide, we’ll be using a very basic example: a Hello World server written with Node.
We’ll also need a package.json, which tells Node some basic things about our application.
To be able to build a Docker image with our app, we’ll need a Dockerfile. You can think of it as a blueprint for Docker: it tells Docker what the contents and parameters of our image should be.

Docker images are often based on other images. For this exercise, we are basing our image on the official Node Docker image. This makes our job easy, and our Dockerfile very short. The grunt work of installing Node and its dependencies in the image is already done in our base image; we’ll just need to include our application.

The Dockerfile is best stored with the code - this way any changes to it are versioned along with the actual application code.

Additionally, our image inherits the following actions from the official node onbuild image:

**1**.  Copy all files in the current directory to /usr/src/app inside the image.

**2**.  Run npm install to install any dependencies for app (if we had any).

**3**.  Specify npm start as the command Docker runs when the container starts.


## Building the image locally

To build the image on your own computer, navigate to the project directory (the one with your application code and the Dockerfile), and run docker build:

```
docker build . -t getintodevops-hellonode:1

```
This instructs Docker to build the Dockerfile in the current directory with the tag getintodevops-hellonode:1. You will see Docker execute all the actions we specified in the Dockerfile


## Running the image locally

If the above build command ran without errors, **congratulations: your first Docker image is ready!**

Let’s make sure the image works as expected by running it:
```
docker run -it -p 8000:8000 getintodevops-hellonode:1

```
The above command tells Docker to run the image interactively with a pseudo-tty, and map the port 8000 in the container to port 8000 in your machine.

You should now be able to check if the server responds in your local port 8000:
```

curl http://127.0.0.1:8000

```
Assuming it does, you can quit the docker run command with CTRL + C.
