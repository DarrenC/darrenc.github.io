# Maven

- [Maven](#maven)
  - [Books, articles](#books-articles)
  - [POM Reference - exlcuding Dependencies](#pom-reference---exlcuding-dependencies)
    - [Exclusions](#exclusions)
    - [Maven plugin for JaxB](#maven-plugin-for-jaxb)
    - [Maven Goals and Phases](#maven-goals-and-phases)
    - [Maven Assembly plugin](#maven-assembly-plugin)
    - [Maven copy dependencies plugin](#maven-copy-dependencies-plugin)
    - [Options for plugins](#options-for-plugins)
    - [Maven links](#maven-links)

## Books, articles

- Good Reference Book -
    <http://books.sonatype.com/mvnex-book/reference/simple-project-sect-create-simple.html>
- Publishing to maven central repo -
    <https://dzone.com/articles/publish-your-artifacts-to-maven-central>

## POM Reference - exlcuding Dependencies

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

### Maven plugin for JaxB

- <https://github.com/highsource/maven-jaxb2-plugin>

Welcome to the org.jvnet.jaxb2.maven2:maven-jaxb2-plugin, the most
advanced and feature-full Maven plugin for XML Schema compilation.

This Maven plugin wraps and enhances the JAXB Schema Compiler (XJC) and
allows compiling XML Schemas (as well as WSDL, DTDs, RELAX NG) into Java
classes in Maven builds.

### Maven Goals and Phases

- <https://www.baeldung.com/maven-goals-phases>

Basic idea: Maven has build lifecycle made of phases, which are made up
of goals.

### Maven Assembly plugin

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

### Maven copy dependencies plugin

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

### Options for plugins

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

### Maven links

- <https://www.baeldung.com/maven>
- <https://www.baeldung.com/maven-profiles>
- <https://www.baeldung.com/executable-jar-with-maven>
