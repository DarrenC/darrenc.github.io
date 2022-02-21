# Java - Quarkus

- [Java - Quarkus](#java---quarkus)
  - [Log-Levels](#log-levels)

## Log-Levels

- <https://quarkus.io/guides/logging>

```properties
# Inside application.properties ...

# Standard quarkus global level
quarkus.log.level=INFO
# particular packages
quarkus.log.category."org.apache".level=DEBUG

```
