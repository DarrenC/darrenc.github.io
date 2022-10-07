# Docker

- [Docker](#docker)
  - [Overview](#overview)
  - [Articles](#articles)
    - [Trainings](#trainings)
  - [Installing](#installing)
  - [Basic commands](#basic-commands)
    - [Starting and stopping containers](#starting-and-stopping-containers)
    - [Using network host](#using-network-host)
  - [Volumes and Mounting](#volumes-and-mounting)
  - [Port Forwarding and server logs](#port-forwarding-and-server-logs)
  - [Dockerfiles](#dockerfiles)
    - [Simple Dockerfile](#simple-dockerfile)
    - [Dockerfile with EXPOSE for php dev server](#dockerfile-with-expose-for-php-dev-server)
  - [Push to dockerhub example](#push-to-dockerhub-example)
  - [Docker-compose files](#docker-compose-files)
    - [Workaround for issues with VPN and address pools](#workaround-for-issues-with-vpn-and-address-pools)
    - [Working with a pre-defined image and mapping volumes](#working-with-a-pre-defined-image-and-mapping-volumes)
    - [Extending a predefined image with Dockerfile + docker-compose](#extending-a-predefined-image-with-dockerfile--docker-compose)
  - [Really simple HelloWorld java cmd line](#really-simple-helloworld-java-cmd-line)
  - [Running containers as different users](#running-containers-as-different-users)
  - [Example from openapi2puml for working with a jar](#example-from-openapi2puml-for-working-with-a-jar)
    - [Volumes and sharing between docker container and host](#volumes-and-sharing-between-docker-container-and-host)
    - [Experience with openapi2puml and volumes](#experience-with-openapi2puml-and-volumes)
  - [Working with Image Repositories (e.g. dockerhub](#working-with-image-repositories-eg-dockerhub)
    - [Pushing an image to dockerhub](#pushing-an-image-to-dockerhub)
    - [Getting a list of all the tags on dockerhub](#getting-a-list-of-all-the-tags-on-dockerhub)
  - [Issues with docker on WSL2](#issues-with-docker-on-wsl2)
    - [Issue with mapping a data dir for mysql using a volume](#issue-with-mapping-a-data-dir-for-mysql-using-a-volume)
  - [TCPDump with Docker containers](#tcpdump-with-docker-containers)
    - [Related Articles for TCPDUMP](#related-articles-for-tcpdump)
  - [JMX and docker containers](#jmx-and-docker-containers)

## Overview

Docker is a container engine built on LXC tech - VE implementations of Linux environments.

## Articles

- Docker mainsite link with install + Python example - <https://docs.docker.com/get-started/part2/>
- <https://stackify.com/guide-docker-java/>
- <https://hub.docker.com/_/openjdk>
- <https://www.jetbrains.com/help/idea/run-and-debug-a-spring-boot-application-using-docker-compose.html>
- <https://medium.com/faun/dockerize-your-java-application-ec7ac056d066>
- <https://stackoverflow.com/questions/35061746/run-jar-file-in-docker-image>
- <https://stackoverflow.com/questions/49382277/docker-jar-not-found>
- <https://forums.docker.com/t/access-docker-container-files/28906> -
    possible soln for issue of paths and jars
- [Nice overview of building java apps with docker including multi-stage](https://blog.frankel.ch/hitchhiker-guide-containerizing-java-apps/)
- [Overview of docker by a fullstack-dev](https://blog.andrewray.me/towards-a-strong-mental-model-of-docker/)
- [Building docker images with small final size](https://phoenixnap.com/kb/docker-image-size)

### Trainings

- [Docker, Dockerfile, and Docker-Compose (2020 Ready!)](https://learning.oreilly.com/videos/docker-dockerfile-and/9781800206847/9781800206847-video3_3)

- Tip - use the docs on dockerhub to see how to use the images
  - [MySQL image](https://hub.docker.com/_/mysql)

## Installing

- Installing on RHEL (with CentOS packages) <https://bytexd.com/how-to-install-docker-on-rhel/>
- Moving the default storage locatin - <https://www.guguweb.com/2019/02/07/how-to-move-docker-data-directory-to-another-location-on-ubuntu/>

## Basic commands

### Starting and stopping containers

```bash

# Run a docker image interactively and connecting with bash terminal, downloading if necessary
docker run -it ubuntu /bin/bash

# Run with a name, detached and will rm the container on exit
docker run -it -d --rm --name linux1 ubuntu /bin/bash

# List all containers
docker ps
docker ps -a # list even stopped containers

# start/stop a container
docker start <container id>
docker stop <container id>

# attach to a running container
docker attach <container id>
docker attach <container name>

# remove a container
docker rm <container id>
-f # force the removal of the container

```

- Can override the CMD from the dockerfile when running (eg run shell
    to see structure of container).

```bash
# build the image
sudo docker build -t openapi2puml-test-image .

# run the container in interactive terminal mode (-it) and override CMD with bash shell
sudo docker run -it openapi2puml-test-image /bin/bash

# run the container normally
sudo docker run -it openapi2puml-test-image

# can also run an image id
docker run ab09184bcb23

# run with an env file in input and detached to not take the terminal
docker run -d \--env-file .env ab09184bcb23

# Seeing running docker containers
docker ps

# Connecting to the box
docker exec -ti <container id from docker ps> bash

# Docker compose with detached and select container to start
$ docker-compose up -d <service or container name>
$ docker-compose down

# tailing the container log
$ docker logs -f <container id>

# Example following a container log and grepping to wait for a particular output
docker logs --follow '${container}' 2>&1 | grep --max-count=1 'I am alive at'

# killing all running containers with a specific ancestor
docker kill $(docker ps -f "ancestor=dockerhub.blah.net:5000/com/com-helloWorldDocker" -a -q)

# docker prune
docker container prune
docker image prune
docker network prune --force # good to run every so often to get rid of conflicting networks from old runs

# docker image delete
# TODO

# See the configuration of the docker container
docker inspect <container_id>


# Get the IP address for a running container, searching by image name
docker inspect --format='{{.NetworkSettings.IPAddress}}' $(docker ps -f ancestor=myImageName --format "{{.ID}}")

```

### Using network host

- Tutorial on docker site <https://docs.docker.com/network/network-tutorial-host/>
  - Basically it's a way to use the host (i.e. something like localhost) to be the docker network instead of configuring a real docker network separately.

## Volumes and Mounting

```bash
# outputting an ls to a file on the host (NB --rm to remove once done)
docker run --rm -v ${PWD}:/myvol ubuntu /bin/bash -c "ls -lha > /myvol/myfile.txt"

# docker run with setting working directory - like doing cd <dir> inside the docker container
docker run ... -w <dir>

# Dockerfile ENTRY_POINT is a command to run when starting the containerf
ENTRYPOINT ["rar"]

# --rm to remove the container after the run....
docker run -it --rm --name my-running-script php:7.2-cli /bin/bash

# Nice example to show form of docker run <options> <image - php:7.2-cli> <cmd - phpindex.php> to output result of running a php file
docker run -it --rm -v ${PWD}:/myfiles -w /myfiles --name my-running-script php:7.2-cli phpindex.php

```

## Port Forwarding and server logs

```bash
# Run a httpd daemon with -p to forward HOST port 8080 to GUEST(container) port 80 - can browse to http://localhost:8080 from local machine
docker run -d -p 8080:80 httpd

```

## Dockerfiles

### Simple Dockerfile

```bash

# Simple Dockerfile (index.php created already in the same dir)
FROM php:7.2-cli

RUN mkdir /myproject
COPY index.php /myproject
WORKDIR /myproject

CMD php index.php

# build image with tag myphpapp - . indicates Dockerfile found in this directory
docker build -t myphpapp .
docker run myphpapp

# listing images and deleting them (nb need to remove containers first)
docker image ls
docker rmi <tag>
```

### Dockerfile with EXPOSE for php dev server

- [Link to docker docs EXPOSE](https://docs.docker.com/engine/reference/builder/#expose)
  - "-P" publishes all ports
  - Otherwise map with -p
  - If the base image (something like php-apache) already exposes a port, you can just do the mapping, no need to explicity use EXPOSE in your image.

```bash

# Dockerfile with EXPOSE
FROM php:7.2-cli

EXPOSE 8000
RUN mkdir /myproject
COPY index.php /myproject
WORKDIR /myproject

CMD ["php", "-S", "0.0.0.0:8000"]

# build as before
docker build -t myphpapp .

# run with port forward to map host to guest ports
docker run--name myphp-container-p 8080:8000 myphpapp

```

## Push to dockerhub example

```bash
docker login
# Assume you already have an image mycurl and your username is myUser123
docker tag mycurl myUser123/mycurl:latest
# See both local tag + userId/tag created
docker image ls
# push to dockerhub
docker push myUser123/mycurl:latest
# cleanup local images
docker rmi mycurl
docker rmi myUser123/mycurl:latest

```

## Docker-compose files

```bash

# Sample docker-compose.yaml with an associated Dockerfile
version: '3'

services:
  phpapp:
    ports:
      - "8080:80"
    build:
      context: ./
      dockerfile: Dockerfile
# This bit was added for the workaround below
networks:
  default:
    external:
      name: localdev

# start, first time will build
docker-compose up

# force a rebuild 
docker-compose up --build

# clean up containers
docker-compose rm

```

### Workaround for issues with VPN and address pools

```pre
From: https://github.com/docker/for-linux/issues/418

Error received: 
ERROR: could not find an available, non-overlapping IPv4 address pool among the defaults to assign to the network

My recommended work-around is to create a network utilizing an unused private address range on your machine:

docker network create localdev --subnet 10.0.1.0/24

Configure docker compose to use this as an external network. Either adding the following to the compose file or the override file as shown:

$ cat docker-compose.override.yml
version: '3'
networks:
  default:
    external:
      name: localdev


```

### Working with a pre-defined image and mapping volumes

```yaml
# with this version you can make changes on the fly for files in the folder with the docker-compose
version: '3'

services:
  phpapp:
    image: php:7.2-apache
    ports:
      - "8080:80"
    volumes:
      - "./:/var/www/html"

networks:
  default:
    external:
      name: localdev

```

### Extending a predefined image with Dockerfile + docker-compose

The example below will extend the base php-apache image with a bunch of extra modules - e.g mysql

```pre
FROM php:7.2-apache

RUN apt-get -y update \
&& apt-get install -y libicu-dev \
&& docker-php-ext-configure intl \
&& docker-php-ext-install intl

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
```

```yaml
version: '3'

services:
  phpapp:
    build:
      context: ./
      dockerfile: Dockerfile
    image: php:7.2-apache
    ports:
      - "8080:80"
    volumes:
      - "./:/var/www/html"
    container_name: my-php-app

networks:
  default:
    external:
      name: localdev

```

Assuming Docker is already setup...

## Really simple HelloWorld java cmd line

```java
 public class HelloWorld {

      public static void main(String[] args){
          System.out.println("Hello World!!!");
      }

}
```

```bash
# Simple java build
FROM openjdk:11-jdk

ADD . /app WORKDIR /app

RUN ls -l

RUN javac HelloWorld.java

CMD [ "java", "HelloWorld" ]
```

```bash
sudo docker build . -t blah
sudo docker run -t blah
```

## Running containers as different users

By default, everything inside docker runs as root. This can be problematic if files/directories are created since they will be owned by root.

- [Running docker container as non-root user](https://medium.com/redbubble/running-a-docker-container-as-a-non-root-user-7d2e00f8ee15)

## Example from openapi2puml for working with a jar

```bash
# Docker multi-stage build

# 1. Building the App with Maven
FROM maven:3-jdk-11
ADD . /openapi2puml
WORKDIR /openapi2puml

# Just echo so we can see, if everything is there :)
RUN ls -l

# Run Maven build
RUN mvn clean install -DskipTests

# DC - test if we can now see jar\.....
RUN ls -l RUN pwd

# TODO - this part makes the final image include only the JDK but it misses
# the correct copy of the jar to the final image. Currently building the whole project and dumping it to the final image
# Just using the build artifact and then removing the build-container
# FROM openjdk:11-jdk

# DC - copy jar somewhere I can see it
# COPY openapi2puml.jar /openapi2puml/openapi2puml.jar # VOLUME /tmp

# FINAL COMMAND to be executed when a container is created
CMD ["java", "-jar", "/openapi2puml/openapi2puml.jar"]
```

```bash
# build the image
sudo docker build -t openapi2puml-test-image .

# run the container in interactive terminal mode (-it) and override CMD
with bash shell sudo docker run -it openapi2puml-test-image /bin/bash

# run the container normally sudo docker run -it
openapi2puml-test-image
```

### Volumes and sharing between docker container and host

- <https://www.digitalocean.com/community/tutorials/how-to-share-data-between-the-docker-container-and-the-host>
- Accessing local file from container -
    <https://stackoverflow.com/questions/44876778/how-can-i-use-a-local-file-on-container>
- From docker docs for run <https://docs.docker.com/engine/reference/commandline/run/>
  - -> \--env , -e
- <https://stackoverflow.com/questions/30494050/how-do-i-pass-environment-variables-to-docker-containers>

### Experience with openapi2puml and volumes

```bash
# I had to map the full path on the host machine to the full container path to get this to work and to see the generate files outside container afterwards.
$ sudo docker run -v $PWD/examples:/openapi2puml/examples -it openapi2puml-test-image
```

## Working with Image Repositories (e.g. dockerhub

### Pushing an image to dockerhub

```bash
# Create an account on docker hub
$ docker login -u <username>

# docker tag <local image>:<tag version> <dockerhub login>/<repo>:<version tag>
$ docker tag openapi2puml-test-image:latest openapi2puml/openapi2puml:0.0.1
$ docker push openapi2puml/openapi2puml:0.0.1
```

### Getting a list of all the tags on dockerhub

- <https://stackoverflow.com/questions/28320134/how-can-i-list-all-tags-for-a-docker-image-on-a-remote-registry>

## Issues with docker on WSL2

### Issue with mapping a data dir for mysql using a volume

In my case the issue occured when mounting a directory from my c drive when using Windows Subsystem for Linux 2 (WSL2). Mounting a directory from my user directory of the wsl linux system worked fine.

If I understand correctly this seems to be a known issue in docker for windows occurring for named volumes: docker/for-win#4812

## TCPDump with Docker containers

If you need to get tcp dumps of traffic within a docker network (eg.g. multiple containers in docker-compose)

- docker-compose file tells me the ip address used for the network (or defaults to 172.17.0.1)

```yaml
networks:
    mynet:
        driver: "bridge"
        ipam:
            driver: default
            config:
                - subnet: 172.17.0.1/16
                  gateway: 172.17.0.1
```

- On the machine running docker containers we can see the ip address and the associated network name:

```shell
$ ip addr
...
142: br-fe8387ea603a: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:4c:15:26:27 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.20.255.255 scope global br-fe8387ea603a
       valid_lft forever preferred_lft forever
    inet6 fe80::42:4cff:fe15:2627/64 scope link 
       valid_lft forever preferred_lft forever
...       
```

- We get the interface name and put it in tcpdump using:
  - Port number of our application to filter
  - Limiting to 100 records captured
  - Printin contents of the packets with -A

```shell
$ sudo tcpdump -i br-fe8387ea603a port 7323 -c 100 -A

...
PACKETS STUFF HERE -

.M.@.@................b.aZ.M.....b<.....
.gR.E\.WHTTP/1.1 200 OK
Connection: keep-alive
Cache-Control: no-cache, must-revalidate, no-transform, no-store
Content-Type: application/json
Content-Length: 2335
Date: Fri, 18 Jan 2019 15:36:23 GMT
...
```

### Related Articles for TCPDUMP

- Julia Evan's EXCELLENT comic <https://jvns.ca/tcpdump-zine.pdf>
- Nice page of examples giving specifically the case with docker containers <https://faun.pub/snooping-on-container-traffic-in-docker-compose-d34764a01276>
- Using a docker container to run tcpdump within the docker group <https://rmoff.net/2019/11/29/using-tcpdump-with-docker/>
  - Similar (didn't follow this one) <https://xxradar.medium.com/how-to-tcpdump-effectively-in-docker-2ed0a09b5406>
  - Nice docker network explanation + diagram <https://www.freecodecamp.org/news/how-to-get-a-docker-container-ip-address-explained-with-examples/>

## JMX and docker containers

- JMX from machine 1 to JVM running on machine 2 - <https://stackoverflow.com/questions/31257968/how-to-access-jmx-interface-in-docker-from-outside>
- Log4J with JMX - <https://logging.apache.org/log4j/2.x/manual/jmx.html>
