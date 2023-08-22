# Maven

- [Maven](#maven)
  - [Books, articles](#books-articles)
    - [Maven References to quick schemas and tags](#maven-references-to-quick-schemas-and-tags)
  - [Installing](#installing)
    - [Linux](#linux)
  - [POM Reference - excluding Dependencies](#pom-reference---excluding-dependencies)
    - [Exclusions](#exclusions)
  - [Maven plugin for JaxB](#maven-plugin-for-jaxb)
  - [Maven Goals and Phases](#maven-goals-and-phases)
  - [Maven Assembly plugin](#maven-assembly-plugin)
  - [Maven copy dependencies plugin](#maven-copy-dependencies-plugin)
  - [Maven Build Helper plugin](#maven-build-helper-plugin)
  - [Maven Profiles](#maven-profiles)
  - [Multi Module project](#multi-module-project)
  - [Options for plugins](#options-for-plugins)
    - [Example of skipping Dependency analysis](#example-of-skipping-dependency-analysis)
    - [Maven Dependency Tree](#maven-dependency-tree)
  - [MVND - a Maven daemon for building in parallel to speed up compile](#mvnd---a-maven-daemon-for-building-in-parallel-to-speed-up-compile)
  - [Maven logging](#maven-logging)
  - [Maven links](#maven-links)

## Books, articles

- Good Reference Book -
    <http://books.sonatype.com/mvnex-book/reference/simple-project-sect-create-simple.html>
- Publishing to maven central repo -
    <https://dzone.com/articles/publish-your-artifacts-to-maven-central>

### Maven References to quick schemas and tags

- Lifecycles and phases - <http://maven.apache.org/ref/3.8.1/maven-core/lifecycles.html>
- POM element schema structure quick-card - <https://maven.apache.org/ref/3.8.1/maven-model/maven.html>

## Installing

### Linux

Can install from package manager on Ubuntu but to get a newer version you can download + install

- Download - <https://maven.apache.org/download.cgi>
- Install to /opt and symlink

```bash
# may need sudo for some commands
$ wget https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz -P /tmp
$ tar xvf /tmp/apache-maven-3.6.3-bin.tar.gz -C /opt
$ ln -s /opt/apache-maven-3.6.3 /opt/maven

# Possibly permissions update 
sudo chmod -R ugo+rx /opt/apache-maven-3.8.4/

# Set in ~./profile as Maven home and export to path
# export MAVEN_HOME="/opt/maven"
# export PATH=${MAVEN_HOME}/bin:${PATH}
source ~/.profile 
```

## POM Reference - excluding Dependencies

### Exclusions

Exclusions explicitly tell Maven that you don't want to include the
specified project that is a dependency of this dependency (in other
words, its transitive dependency). For example, the maven-embedder
requires maven-core, and we do not wish to use it or its dependencies,
then we would add it as an exclusion.

```xml
<project xmlns="<http://maven.apache.org/POM/4.0.0>"

    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                        http://maven.apache.org/xsd/maven-4.0.0.xsd">
    ...
    <dependencies>
      <dependency>
        <groupId>org.apache.maven</groupId>
        <artifactId>maven-embedder</artifactId>
        <version>2.0</version>
        <exclusions>
          <exclusion>
            <groupId>org.apache.maven</groupId>
            <artifactId>maven-core</artifactId>
          </exclusion>
        </exclusions>
      </dependency>
      ...
    </dependencies>
    ...

</project>
```

It is also sometimes useful to clip a dependency's transitive
dependencies. A dependency may have incorrectly specified scopes, or
dependencies that conflict with other dependencies in your project.
Using wildcard excludes makes it easy to exclude all a dependency's
transitive dependencies. In the case below you may be working with the
maven-embedder and you want to manage the dependencies you use yourself,
so you clip all the transitive dependencies:

```xml
<project xmlns="<http://maven.apache.org/POM/4.0.0>"

    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                        http://maven.apache.org/xsd/maven-4.0.0.xsd">
    ...
    <dependencies>
      <dependency>
        <groupId>org.apache.maven</groupId>
        <artifactId>maven-embedder</artifactId>
        <version>3.1.0</version>
        <exclusions>
          <exclusion>
            <groupId>*</groupId>
            <artifactId>*</artifactId>
          </exclusion>
        </exclusions>
      </dependency>
      ...
    </dependencies>
    ...

</project>
```

- exclusions:
  - Exclusions contain one or more exclusion elements, each containing a groupId and artifactId denoting a dependency to exclude. Unlike optional, which may or may not be installed and used, exclusions actively remove themselves from the dependency tree.

## Maven plugin for JaxB

- <https://github.com/highsource/maven-jaxb2-plugin>

Welcome to the org.jvnet.jaxb2.maven2:maven-jaxb2-plugin, the most
advanced and feature-full Maven plugin for XML Schema compilation.

This Maven plugin wraps and enhances the JAXB Schema Compiler (XJC) and
allows compiling XML Schemas (as well as WSDL, DTDs, RELAX NG) into Java
classes in Maven builds.

## Maven Goals and Phases

- <https://www.baeldung.com/maven-goals-phases>

Basic idea: Maven has build lifecycle made of phases, which are made up
of goals.

## Maven Assembly plugin

Can be used to build executable jars, zips etc. In general can be
replaced by the maven shadow plugin for building an "uberjar" but
helpful for building a zip containing all code - tests and main classes
for example which shadow can't do.

- Nice description and examples -
    <https://people.apache.org/~epunzalan/maven-assembly-plugin/usage.html>
- <https://maven.apache.org/plugins/maven-assembly-plugin/>

NB - normal phase is package, install is for a particular project need.

```bash

mvn org.apache.maven.plugins:maven-assembly-plugin:2.3:single
    -Dassembly.appendAssemblyId=false
    -Ddescriptor=src/main/assembly/assembly_uberjar.xml
    -DfinalName=gatling

mvn org.apache.maven.plugins:maven-assembly-plugin:2.3:single
    -Dassembly.appendAssemblyId=false
    -Ddescriptor=src/main/assembly/assembly_zip.xml
    -DfinalName=gatlingCommandLine

```

```xml
    <plugin>
      <artifactId>maven-assembly-plugin</artifactId>
      <version>2.3</version>
      <executions>
          <execution>
              <id>make-assembly-uberjar</id>
              <phase>install</phase>
              <goals>
                  <goal>single</goal>
              </goals>
              <configuration>
                  <descriptor>src/main/assembly/assembly_uberjar.xml</descriptor>
                  <finalName>gatling</finalName>
                  <appendAssemblyId>false</appendAssemblyId>
              </configuration>
          </execution>
          <execution>
              <id>make-assembly-zip</id>
              <phase>install</phase>
              <goals>
                  <goal>single</goal>
              </goals>
              <configuration>
                  <descriptor>src/main/assembly/assembly_zip.xml</descriptor>
                  <finalName>gatlingCommandLine</finalName>
                  <appendAssemblyId>false</appendAssemblyId>
              </configuration>
          </execution>
      </executions>
    </plugin>
```

## Maven copy dependencies plugin

- Can be used to copy dependencies and even recreate the structure of the repo + pom files etc.
  - <http://maven.apache.org/plugins/maven-dependency-plugin/copy-dependencies-mojo.html>
- Interesting first answer showing how to copy structure + run from
    command-line

NB - normal phase is package, install is for a particular project need.

```bash
mvn org.apache.maven.plugins:maven-dependency-plugin:3.1.2:copy-dependencies
    -DoutputDirectory=../DCRepo
    -Dmdep.useRepositoryLayout=true
    -Dmdep.copyPom=true -DoverWriteIfNewer=true
```

```xml
<plugin>

  <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-dependency-plugin</artifactId>
      <version>3.1.2</version>
      <executions>
          <execution>
              <id>copy-dependencies</id>
              <phase>install</phase>
              <goals>
                  <goal>copy-dependencies</goal>
              </goals>
              <configuration>
                  <outputDirectory>../DCRepo</outputDirectory>
                  <useRepositoryLayout>true</useRepositoryLayout>
                  <copyPom>true</copyPom>
                  <overWriteReleases>false</overWriteReleases>
                  <overWriteSnapshots>false</overWriteSnapshots>
                  <overWriteIfNewer>true</overWriteIfNewer>
              </configuration>
          </execution>
      </executions>
  </plugin>

```

## Maven Build Helper plugin

Can be useful to "add" sources or tests to the list of files to be considered for a compile. Works in a "generate-sources" phase before the build.

- <https://stackoverflow.com/questions/6025596/conditional-exclusion-of-file-from-compilation-in-maven-project>
- Quick description - <https://www.mojohaus.org/build-helper-maven-plugin/add-source-mojo.html>
- How to use it - <https://www.mojohaus.org/build-helper-maven-plugin/usage.html>

I've made use of it in a profile to add back an excluded source to the build.

## Maven Profiles

You can build differently depending on the required context - e.g. environment diffs etc.

- <https://maven.apache.org/guides/introduction/introduction-to-profiles.html>
- <https://maven.apache.org/guides/mini/guide-building-for-different-environments.html>

```shell
# Basic usage
mvn groupId:artifactId:goal -P profile-1,profile-2,?profile-3
mvn clean package -P build_for_test
```

## Multi Module project

- <https://www.baeldung.com/maven-multi-module>
  - Example of having multiple modules in a project

## Options for plugins

From the maven docs it can be difficult to work out what the command
line options are, especially when the xml and command line formats are
slightly different. Checking the source code can give you the definitive
guide to what to use:

- Gatling maven plugin - <https://gatling.io/docs/2.2/extensions/maven_plugin/>
  - e.g. <https://github.com/gatling/gatling-maven-plugin/blob/master/src/main/java/io/gatling/mojo/GatlingMojo.java>

```bash

# Run a single named test from mvn
mvn gatling:test -Dgatling.simulationClass=org.blah.SomeGatlingSimulationClassName

# Enable multiple simulations to be run from gatling mvn plugin - could also do on command line I think:
# <configuration>
#   <runMultipleSimulations>true</runMultipleSimulations>
# </configuration>
```

### Example of skipping Dependency analysis

```bash
# https://maven.apache.org/plugins/maven-dependency-plugin/analyze-mojo.html#skip
mvn -Dmdep.analyze.skip=true clean deploy
```

### Maven Dependency Tree

```bash
$ mvn dependency:tree
        ....
        [INFO] com.restapi:msproducts:jar:0.0.1-SNAPSHOT
        [INFO] +- org.springframework.boot:spring-boot-starter-data-jpa:jar:2.2.6.RELEASE:compile
        [INFO] |  +- org.springframework.boot:spring-boot-starter-aop:jar:2.2.6.RELEASE:compile
        [INFO] |  |  +- org.springframework:spring-aop:jar:5.2.5.RELEASE:compile
        [INFO] |  |  \- org.aspectj:aspectjweaver:jar:1.9.5:compile
        [INFO] |  +- org.springframework.boot:spring-boot-starter-jdbc:jar:2.2.6.RELEASE:compile
        [INFO] |  |  +- com.zaxxer:HikariCP:jar:3.4.2:compile
        [INFO] |  |  \- org.springframework:spring-jdbc:jar:5.2.5.RELEASE:compile
        [INFO] |  +- jakarta.activation:jakarta.activation-api:jar:1.2.2:compile
        [INFO] |  +- jakarta.persistence:jakarta.persistence-api:jar:2.2.3:compile
        [INFO] |  +- jakarta.transaction:jakarta.transaction-api:jar:1.3.3:compile
        [INFO] |  +- org.hibernate:hibernate-core:jar:5.4.12.Final:compile
```

```bash
# Can filter to search for or exclude dependencies
$ mvn dependency:tree -Dincludes=org.projectlombok

        [INFO] --- maven-dependency-plugin:3.1.2:tree (default-cli) @ msproducts ---
        [INFO] com.restapi:msproducts:jar:0.0.1-SNAPSHOT
        [INFO] \- org.projectlombok:lombok:jar:1.18.12:compile (optional)

$ mvn dependency:tree -Dexcludes=org.springframework.*,org.projectlombok
```

Also more here -

- use verbose mode (useful for conflicts), filter examples <https://devwithus.com/maven-dependency-tree/>
- Official docs - <https://maven.apache.org/plugins/maven-dependency-plugin/tree-mojo.html>

## MVND - a Maven daemon for building in parallel to speed up compile

- <https://github.com/apache/maven-mvnd>

## Maven logging

- <https://www.baeldung.com/maven-logging>

```bash
mvn --log-file ./mvn.log clean compile

```

## Maven links

- <https://www.baeldung.com/maven>
- <https://www.baeldung.com/maven-profiles>
- <https://www.baeldung.com/executable-jar-with-maven>
