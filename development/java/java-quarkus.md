# Java - Quarkus

- [Java - Quarkus](#java---quarkus)
  - [Log-Levels](#log-levels)
  - [MicroProfile Rest Client vs Server side Jax-RS](#microprofile-rest-client-vs-server-side-jax-rs)

## Log-Levels

- <https://quarkus.io/guides/logging>

```properties
# Inside application.properties ...

# Standard quarkus global level
quarkus.log.level=INFO
# particular packages
quarkus.log.category."org.apache".level=DEBUG
```

## MicroProfile Rest Client vs Server side Jax-RS

- Standard JAX-RS - Server side to map Exception to Response - javax.ws.rs.ext.ExceptionMapper
- MicroProfile Rest Client - org.eclipse.microprofile.rest.client.ext.ResponseExceptionMapper client side inverse
  - Default ResponseExceptionMapper throws a WebApplicationException for any Response with status >= 400
