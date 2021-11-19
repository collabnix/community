### Building your first Docker image with Jenkins 2

![](https://collabnix.com/wp-content/uploads/2018/03/ci-cd.png)

Containerising your application is like shoving your app and all its dependencies into a box. Except the box is infinitely replicable. Whatever happens in the box, stays in the box - unless you explicitly take something out or put something in. And when it breaks, you’ll just throw it away and get a new one.

**Containers** make your app easy to run on different computers - ideally, the same image should be used to run containers in every environment stage from development to production.

This project is your guide for building a Docker image, and then setting up Jenkins 2 to build and publish the image automatically, whenever you commit changes to your code repository.

###  Requirements

To run through this guide, you will need the following:

**1**. To build and run the Docker image locally: Mac OS X or Linux, and Docker installed
**2**. To set up Jenkins to build the image automatically: Access to a Jenkins 2.x installation ![](https://www.jenkins.io/doc/book/installing/) you could run it as a container, see instructions here)

