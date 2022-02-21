# HSQLDB Database

- Very OLD now

Very useful database that can be used for dev/testing to get up and
running v quickly. Its a java based DB that runs in memory. Basically
all you need is the hsqldb.jar file which can then be run like a
standard java app on the command line. There are various startup options
to make the DB run completely in memory or as a standalone server with
the data being saved off to files for future use.

## From within your App

in Hibernate configuration File:

For completely in memory DB:

```xml
  <session-factory>
    <property name="hibernate.connection.driver_class">org.hsqldb.jdbcDriver</property>
    <property name="hibernate.connection.url">jdbc:hsqldb:mem:foobar</property>
    <property name="hibernate.connection.username">sa</property>
    <property name="hibernate.dialect">org.hibernate.dialect.HSQLDialect</property>
        .
        .
        .
  </session-factory>
```

Or to connect to a standalone instance running elsewhere:

```xml
  <session-factory>
    <property name="hibernate.connection.driver_class">org.hsqldb.jdbcDriver</property>
    <property name="hibernate.connection.url">jdbc:hsqldb:hsql://localhost</property>
    <property name="hibernate.connection.username">sa</property>
    <property name="hibernate.dialect">org.hibernate.dialect.HSQLDialect</property>
        .
        .
        .
  </session-factory>
```

### Standalone

Running a stand alone HSQLDB in another command window:

- With Maven
  - HibernateMavenTutorial$ mvn exec:java -Dexec.mainClass="org.hsqldb.Server" -Dexec.args="-database.0 file:target/data/tutorial"

- From a command line
  - $java -classpath lib/hsqldb.jar org.hsqldb.Server

This allows you to persist the DB between runnings of the database.
Otherwise you can just use an in-memory HSQLDB

### Utilities

HSQLDB comes with some utilities for operations on the database

- HSQL DB Manager (Swing based) :
  - mvn exec:java -Dexec.mainClass=\"org.hsqldb.util.DatabaseManagerSwing\"
