# Docker

- [Docker](#docker)
  - [Basic commands](#basic-commands)
  - [Really simple HelloWorld java cmd line](#really-simple-helloworld-java-cmd-line)
  - [Example from openapi2puml for working with a jar](#example-from-openapi2puml-for-working-with-a-jar)
    - [Volumes and sharing between docker container and host](#volumes-and-sharing-between-docker-container-and-host)
    - [Experience with openapi2puml and volumes](#experience-with-openapi2puml-and-volumes)
  - [Pushing an image to dockerhub](#pushing-an-image-to-dockerhub)

- Docker mainsite link with install + Python example -
    <https://docs.docker.com/get-started/part2/>
- <https://stackify.com/guide-docker-java/>
- <https://hub.docker.com/_/openjdk>
- <https://www.jetbrains.com/help/idea/run-and-debug-a-spring-boot-application-using-docker-compose.html>
- <https://medium.com/faun/dockerize-your-java-application-ec7ac056d066>
- <https://stackoverflow.com/questions/35061746/run-jar-file-in-docker-image>
- <https://stackoverflow.com/questions/49382277/docker-jar-not-found>
- <https://forums.docker.com/t/access-docker-container-files/28906> -
    possible soln for issue of paths and jars

## Basic commands

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
$ docker-compose up -d sos
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

## Pushing an image to dockerhub

```bash
# Create an account on docker hub
$ docker login -u <username>

# docker tag <local image>:<tag version> <dockerhub login>/<repo>:<version tag>
$ docker tag openapi2puml-test-image:latest openapi2puml/openapi2puml:0.0.1
$ docker push openapi2puml/openapi2puml:0.0.1
```
