# Learning Project

## Overview

- Learning project to explore some new tech and keep up to date on
    full stack stuff
  - Angular
  - Springboot
  - JPA
  - Gradle
  - Docker
  - TODO - add tooling here, IDE, java versions, git etc.

          * git setup - used windows version to have the bash
          * Starting out by installing in windows but could be interesting to use the docker stuff under ubuntu

## First steps - Setup new machine

### Java install

- What version to choose:
  - At work we're using Java8 Oracle so wouldn't mind trying out
        something else
  - OpenJDK11 seems like a good place to start.
  - <https://en.wikipedia.org/wiki/Java_version_history>

- I kept things simple, unzipped OpenJDK11 to DCDev and created
    JAVA_HOME and added to PATH

### Gradle install

I haven't worked with it before so I have a lot to learn here.

- Guides for building different types of projects -
    <https://gradle.org/guides/>
- <https://gradle.org/install/>

The install for windows is done manually It seems also that the Spring
gradle guide is out of date compared to the latest gradle guide where
there's a gradle init to setup and standard java project structure
etc\....

- <https://guides.gradle.org/building-java-applications/>

### Commands

### Tips from Arnaud

OReilly "Web application development with Spring and Angular"

### Start Development

### Springboot

- Basic tutorial with gradle/maven etc.
  - <https://spring.io/guides/gs/spring-boot/>
  - <https://spring.io/guides/gs/gradle/>
    - really old 2.13 vs actual 5.4.1 - issues when using the
            gradlew commands since my JDK 11 was not compatible.
  - <https://spring.io/guides/gs/spring-boot-docker/>

## Link dump - Event driven project + cloud TODO

- <http://www.benstopford.com/2018/06/07/rest-request-response-gateway/> - DONE
- <https://docs.microsoft.com/en-us/azure/architecture/patterns/sidecar> - DONE
- <https://github.com/dapr/dapr> - DONE
- <https://dapr.io> - DONE
- <https://vertx.io/introduction-to-vertx-and-reactive/> - DONE BUT WORTH A SECOND LOOK
- <https://smallrye.io/smallrye-reactive-messaging/smallrye-reactive-messaging/3.9/concepts.html> DONE
- <https://developer.lightbend.com/docs/introduction/traditional-architecture.html> - DONE
- <https://en.wikipedia.org/wiki/Service-oriented_architecture> - DONE
- <https://martinfowler.com/articles/microservices.html#footnote-etymology>
  - READ
    - Follow ons
      - <https://martinfowler.com/bliki/TolerantReader.html>
      - <https://martinfowler.com/articles/consumerDrivenContracts.html>

- <https://www.ibm.com/cloud/blog/soa-vs-microservices> - DONE (NOT GOOD)
- <https://www.progress.com/blogs/the-relationship-between-cep-eda-and-soa> - DONE (NOT GOOD)
- <https://quarkus.io/guides/rest-client>
- <https://kafka.apache.org/20/documentation/streams/developer-guide/testing.html>
- <https://www.reddit.com/r/apachekafka/comments/seifte/kafka_learning_path/>
- <https://quarkus.io/guides/getting-started>
- <https://medium.com/swlh/apache-kafka-in-a-nutshell-5782b01d9ffb>
- Kafka Cheatsheet - <https://thecodinginterface.com/blog/kafka-cli-cheat-sheet/>
- ArgoCD - gitops style continuous deployment - <https://argo-cd.readthedocs.io/en/stable/>
- Loom virtual threads in Quarkus - <https://developers.redhat.com/devnation/tech-talks/integrate-loom-quarkus>
- Reactive in Quarkus - TODO mutiny vs Completable future - <https://quarkus.io/guides/quarkus-reactive-architecture>
  - Apparently mutiny is more truly reactive
  - but sometimes need both - <https://medium.com/@alexei.rubinov/combining-smallrye-mutiny-and-completionstage-approach-in-quarkus-ec23751578b9>
  - Comparing them + suggesting use cases e.g. single microservice collateral call vs stream of calls - <https://www.jrebel.com/blog/java-completablefuture-api>

### Event driven vs Reactive

- Event driven is from process based events, Reactive is data driven - reacting to the change of a data value.

### Fibre optic

- <https://lafibre.info/raccordement-maison/maison-au-fond-dun-passage-de-10-maisons/>
- <https://reseaux.orange.fr/maison/comment-avoir-fibre>