---
title: "Using Jenkins"
linkTitle: "Using Jenkins"
weight: 101
description: >-
     Continuous Integration Pipeline using Docker, Jenkins & GitHub 
---


Continuous Integration (CI) is a development practice that requires developers to integrate code into a shared repository several times a day. Each check-in is then verified by an automated build, allowing teams to detect problems early. CI doesn’t get rid of bugs, but it does make them dramatically easier to find and remove.

CI/CD merges development with testing, allowing developers to build code collaboratively, submit it the master branch, and checked for issues. This allows developers to not only build their code, but also test their code in any environment type and as often as possible to catch bugs early in the applications development lifecycle. Since Docker can integrate with tools like Jenkins and GitHub, developers can submit code in GitHub, test the code and automatically trigger a build using Jenkins, and once the image is complete, images can be added to Docker registries. This streamlines the process, saves time on build and set up processes, all while allowing developers to run tests in parallel and automate them so that they can continue to work on other projects while tests are being run.

A Typical CI workflow look like:

![image](https://user-images.githubusercontent.com/313480/141933310-8b0f778c-7f95-4484-aa55-b89a4edf2110.png)




1. Developer pushes a commit to GitHub
2. GitHub uses a webhook to notify Jenkins of the update
3. Jenkins pulls the GitHub repository, including the Dockerfile describing the image, as well as the application and test code.
4. Jenkins builds a Docker image on the Jenkins slave node
5. Jenkins instantiates the Docker container on the slave node, and executes the appropriate tests
6. If the tests are successful the image is then pushed up to Dockerhub or Docker Trusted Registry.

Under these series of blog post, I will help you get started with Continuous Integration with Jenkins, Docker & GitHub under $0. I will be using Play with Docker platform which comes for free for the general public.

Let’s get started..

Go to your browser and type –  https://labs.play-with-docker.com/

![image](https://user-images.githubusercontent.com/313480/141933373-31bcc826-5031-4326-83c8-43c0ee6d10d1.png)


 

### Open up a “New Instance” on the left hand side of the screen.

![image](https://user-images.githubusercontent.com/313480/141933397-34930488-3a5c-46fc-82f6-85e261171317.png)

 



 

## Cloning the Repository

Let us start with a simple HTML webpage application. I have a sample GITHUB repository already created for you which contains Dockerfile and Jenkinsfile under the root of the repository as shown below:

![image](https://user-images.githubusercontent.com/313480/141933429-2159bdf2-64c3-43c1-ac63-1d36b2782064.png)


 

 

```
$ git clone https://github.com/ajeetraina/webpage
```
 

## What is Jenkinsfile & Jenkins Pipeline?

A Jenkinsfile is a text file that contains the definition of a Jenkins Pipeline and is checked into source control.

Jenkins Pipeline (or simply “Pipeline”) is a suite of plugins which supports implementing and integrating continuous delivery pipelines into Jenkins. It provides an extensible set of tools for modeling simple-to-complex delivery pipelines “as code”. The definition of a Jenkins Pipeline is typically written into a text file (called a Jenkinsfile) which in turn is checked into a project’s source control repository.
I have created a sample Jenkinsfile which clones the repository, builds the Docker Image, test it and then push it to Dockerhub automatically using Jenkins.

```
 node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("ajeetraina/webpage")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * Just an example */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
```

In the above Jenkinsfile, there are various stages like cloning the SCM, build, test and pushing the Docker image. You will need to change it to your respective GITHUB repo if you want to try to build your own Docker image.

Let us quickly setup Jenkins on PWD platform and believe me it’s just a matter of a single docker-compose CLI. Before we proceed, ensure that the below permission is granted so as to get Docker plugin to work flawlessly –

```
$chmod 666 /var/run/docker.sock
```

It’s time to clone the repository:

```
$ git clone https://github.com/ajeetraina/jenkins
Cloning into ‘jenkins’…
remote: Counting objects: 18, done.
remote: Compressing objects: 100% (16/16), done.
remote: Total 18 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (18/18), done.
[node1] (local) root@192.168.0.53 ~/webpage
```

```
$ cd jenkins
[node1] (local) root@192.168.0.53 ~/webpage/jenkins
$docker-compose up
```
![image](https://user-images.githubusercontent.com/313480/141933566-d3b4718d-504c-4c1a-8a5e-efb4c4771275.png)


Copy the password of the jenkins starting with “5ee571..” as shown in the above screenshot.

Click on 8080 port which appear on the top of the screen and this will redirect you to Jenkins page.

![image](https://user-images.githubusercontent.com/313480/141933585-c833f471-cc8c-49b8-a31c-319df4f33fa9.png)


Once you add the Administrator password which we copied earlier, then it will ask to install plugins. Choose “Install Suggested Plugins” on the left hand side as shown below:


![image](https://user-images.githubusercontent.com/313480/141933610-89ef6113-5a9c-43c4-b8a7-7979262e3b6c.png)

![image](https://user-images.githubusercontent.com/313480/141933656-9d21a947-d344-47be-ab46-3623aff7cd40.png)


![image](https://user-images.githubusercontent.com/313480/141933676-15894c43-101d-4362-912b-a47f81bd6017.png)



Go back to Jenkins dashboard and click “New Item”. Supply any name(i.e demo-webpage) and select “Pipeline” as type of the project.

![image](https://user-images.githubusercontent.com/313480/141933696-00061ee6-d925-40fe-8447-7d1f86618b20.png)


This will show up a page with Build Triggers as one of the option. Select “Pipeline script from SCM” and choose GIT under SCM. This will allow you to enter your GITHUB URL which in my case is https://github.com/ajeetraina/webpage. This will automatically add Jenkinsfile under Script Path. Click on “Apply” and then Save.

![image](https://user-images.githubusercontent.com/313480/141933718-5458c69d-ff85-4055-b2c2-1020af8e19af.png)


Click on “Build Now” option on the left side of the Jenkins screen. This traverse through the build pipeline i.e cloning the repository, building Docker Image , testing it and pushing it to your Dockerhub account as shown below:

![image](https://user-images.githubusercontent.com/313480/141933736-505e0093-e936-4468-aec2-9be41721f43b.png)
 



 

 

 

Once you click on “Build Now” you will see that it initiates the build pipeline.


![image](https://user-images.githubusercontent.com/313480/141933757-e688604d-0e82-4497-a263-2603853a6a0b.png)

 

## Jenkins Pipeline Stages View:


![image](https://user-images.githubusercontent.com/313480/141933776-2bb08e2b-d1de-4679-9f55-f6c26c2b022d.png)

 

Click on “Console Output” to show detailed build process as shown below:


![image](https://user-images.githubusercontent.com/313480/141933789-a60169f1-0e26-4aca-8284-2353f2be64d1.png)

 

## A Quick View of Stage View:

 
![image](https://user-images.githubusercontent.com/313480/141933807-d1c53cd5-bec3-41e5-8b66-d916134fd00c.png)



 

Till now, we have a new Docker Image pushed to Dockerhub automatically. Let’s go ahead and verify it by bringing up webpage container in the separate instance window as shown below:

 
![image](https://user-images.githubusercontent.com/313480/141933827-ee10fd1e-c391-47b6-87f8-88529ffc5886.png)



 

Here you see…a static HTML page appears running on port 80. This was built as part of Jenkins pipeline.


![image](https://user-images.githubusercontent.com/313480/141933845-162efd23-ce38-4ac9-bbe8-e9d9c6d4c178.png)

In order to trigger this pipeline every 15 minutes, you can go back to Jenkins page for specific job and then choose “Build Periodically” under Configure page as shown below:

![image](https://user-images.githubusercontent.com/313480/141933874-8192f705-5d89-4b2a-977f-eb199ff08582.png)
