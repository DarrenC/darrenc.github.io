# Overview

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
