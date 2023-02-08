---
layout: default
title: Docker compose
description: collabnix | DockerLab | Docker compose
---

# Docker compose

Docker compose is a tool built by docker to ease the task to creating and configring multiple containers in a development environment counter-part of docker-compose for prodcution environment is `docker swarm`. Docker compose takes as input a `YAML` configuration file and creates the resources (*containers*, *networks*, *volumes* etc.) by communicating with the docker daemon through docker api.

## Compose file used in examples

```yaml
version: '3'

services:
    web:
        build: .
        image: web-client
        depends_on:
        - server
        ports:
        - "8080:8080"
    server:
        image: akshitgrover/helloworld
        volumes:
        - "/app" # Anonymous volume
        - "data:/data" # Named volume
        - "mydata:/data" # External volume

volumes:
    data:
    mydata:
        external: true
```

Refer [this](https://docs.docker.com/compose/compose-file/) for configuring your compose file.

## CLI Cheatsheet

- [Docker compose](#docker-compose)
  - [Compose file used in examples](#compose-file-used-in-examples)
  - [CLI Cheatsheet](#cli-cheatsheet)
    - [Build](#build)
    - [Bundle](#bundle)
    - [Config](#config)
    - [Up](#up)
    - [Down](#down)
    - [Scale](#scale)
    - [Start](#start)
    - [Stop](#stop)

### Build

Used to build services specified in docker-compose.yml file with `build` specification.

Refer [this](https://docs.docker.com/compose/compose-file/#build) for more details.

**Note:**
Images build will be tagged as {DIR}_{SERVICE} unless image name is specified in the service specification.

```
docker-compose build [OPTIONS] [SERVICE...]

OPTIONS:

--compress | Command line flag to compress the build context, Build context is nothing but a directory where docker-compose.yml file is located. As this directory can container a lot of files, sending build context to the container can take a lot of time thus compression is needed.

--force-rm | Remove any intermediate container while building.

--no-cache | Build images without using any cached layers from previoud builds.

--pull | Allways pull newer version of the base image.

-m, --memory | Set memory limit for the container used for building the image.

--parallel | Exploit go routines to parallely build images, As docker daemon is written in go.

--build-arg key=val | Pass any varaible to the dockerfile from the command line.


SERVICE:

If you want to build any particular services instead of every service specified in the compose file pass the name (same as in the compose file) as arguments to the command.

Example:

docker-compose build --compress     # Will compress the build context of service web.

```

### Bundle

Used to generate distributed application bundle (DAB) from the compose file.

Refer [this](https://docs.docker.com/compose/bundles/) for more details about DBA.

```
docker-compose bundle [OPTIONS]

OPTIONS:

--push-image | Push images to the register if any service has build specifcation.

-o, --output PATH | Output path for .dab file.
```

### Config

Used to validate the compose file

NOTE:
Run this command in direcotry where docker-compose.yml file is located.

```
docker-compose config
```

### Up

Creates and starts the resources as per the specification the docker-compose.yml file.

```
docker-compose up [OPTIONS] [SERVICE...]

OPTIONS:

-d, --detach | Run containers in background.

--build | Always build images even if it exists.

--no-deps | Avoid creating any linked services.

--force-recreate | Force recreating containers even if specification is not changed.

--no-recreate | Do not recreate containers.

--no-build | Do not build any image even if it is missing.

--no-start | Just create the containers without starting them.

--scale SERVICE=NUM | Create multiple containers for a service.

-V, --renew-anon-volumes | Recreate anonymous volumes instead of getting data from previous ones.

Example:

docker-compose up -d        # Will run service containers in background
docker-compose up web       # Will start service web and server because of 'depends_on' field
docker-compose up server    # will start server service only.
```

### Down

Stop and clear any resources created while lifting docker-compose.

By default only containers and networks defined in the compose file are removed.
Networks and Volumes with external = true and never removed.

```
docker-compose down [OPTIONS]

--rmi type | Remove images Type = all (Remove every image in the compose file), local (Remove images with no custom tag)

-v, --volumes | Remove named volumes except the external ones and also remove anonymous volumes

-t, --timeout TIMEOUT | Speficy shutdown time in seconds. (default = 10)

Example:

docker-compose down         # Will delete all containers of both web and server and no volume will be removed

docker-compose down -v      # Will also delete anonymous and data volumes.
```

### Scale

Scale particular services

```
docker-compose scale [SERVICE=NUM...]

Example:

docker-compose scale server=3 web=2
```

### Start

Start created containers.

```
docker-compose start [SERVICE...]

Example:

docker-compose start        # Start containers for every service.
docker-compose start web    # Start containers only for service web. 
```

### Stop

Stop running containers.

```
docker-compose stop [SERVICE...]

Example:

docker-compose stop         # Stop containers for every service.
docker-compose stop web     # Stop containers only for service web.
```

# Docker compose with swarm secrets


Start securing your swarm services using the latest compose reference that allows to specify secrets in your application stack

## Getting started

Make sure your daemon is in swarm mode or initialize it as follows:

```
docker swarm init --advertise-addr $(hostname -i)
```

## Automatic provision

In this example we’ll let compose automatically create our secrets and provision them through compose with the defined secret file

Create a new secret and store it in a file:

```
echo "shh, this is a secret" > mysecret.txt
```

Use your secret file in your compose stack as follows:

```
echo 'version: '\'3.1\''
services:
    test:
        image: '\'alpine\''
        command: '\'cat /run/secrets/my_secret \''
        secrets: 
            - my_secret

secrets:
    my_secret:
        file: ./mysecret.txt
' > docker-compose.yml
```

## Deploy your stack service:

```
docker stack deploy -c docker-compose.yml secret
```

Results in the below output:

```
Creating network secret_default
Creating secret secret_my_secret
Creating service secret_test
```

After your stack is deployed you can check your service output:

```
docker service logs -f secret_test
```

Results in the below output (below values after secret_test.1. may vary):

```
secret_test.1.lcygnppmzfdp@node1    | shhh, this is a secret
secret_test.1.mg1420w2i3x4@node1    | shhh, this is a secret
secret_test.1.8osraz8yxjrb@node1    | shhh, this is a secret
secret_test.1.byh5b9uik6db@node1    | shhh, this is a secret
```

.
.
.

## Using existing secrets

Create a new secret using the docker CLI:

```
echo "some other secret" | docker secret create manual_secret - 
```

Define your secret as external in your compose file so it’s not created while deploying the stack

```
echo 'version: '\'3.1\''
services:
    test:
        image: '\'alpine\''
        command: '\'cat /run/secrets/manual_secret \''
        secrets: 
            - manual_secret

secrets:
    manual_secret:
        external: true
' > external-compose.yml
```

## Deploy your stack as you did in the automatic section:

```
docker stack deploy -c external-compose.yml external_secret
```

## Validate your secret is there by checking the service logs

```
docker service logs -f external_secret_test
```

# Contributors:

@marcosnils [Akshit Grover]()
