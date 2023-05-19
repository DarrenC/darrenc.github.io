# Java - Quarkus

- [Java - Quarkus](#java---quarkus)
  - [Useful Links](#useful-links)
  - [Log-Levels](#log-levels)
  - [MicroProfile Rest Client vs Server side Jax-RS](#microprofile-rest-client-vs-server-side-jax-rs)
    - [Quarkus Reactive programming for RestEasy](#quarkus-reactive-programming-for-resteasy)
    - [Microprofile RestClient Exception handling](#microprofile-restclient-exception-handling)
  - [Scheduling stuff in Quarkus](#scheduling-stuff-in-quarkus)
  - [Remote debug in Quarkus](#remote-debug-in-quarkus)
  - [Quarkus Testing](#quarkus-testing)

## Useful Links

- Cheat sheet - <https://lordofthejars.github.io/quarkus-cheat-sheet/>
- Quarkus - benchmark of native vs JVM - <https://quarkus.io/blog/runtime-performance/>

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
  - Default ResponseExceptionMapper throws a WebApplicationException for any Response with status >= 400 <https://download.eclipse.org/microprofile/microprofile-rest-client-2.0/microprofile-rest-client-spec-2.0.html#_responseexceptionmapper>

### Quarkus Reactive programming for RestEasy

- SUPER IMPORTANT TODO - RESTEasy Reactive in Quarkus- <https://www.youtube.com/watch?v=30eFZGml_-g>
  - This is something we can do to gain performance
  - also intro to mutiny primer - <https://quarkus.io/guides/mutiny-primer>

### Microprofile RestClient Exception handling

When you are working with the microprofile rest client it throws a WebApplicationException for http codes >=400.
If you want to see the content of the Response to get headers etc. you need to create a custom mapper that extends the ResponseExceptionMapper and register it with the rest client by annotation.
This is slightly different to standard JAX-RS (but which uses exception mappers too - <https://dennis-xlc.gitbooks.io/restful-java-with-jax-rs-2-0-2rd-edition/content/en/part1/chapter7/exception_handling.html> or <https://access.redhat.com/documentation/en-us/red_hat_jboss_fuse/6.2.1/html/apache_cxf_development_guide/restexceptionmapper>)

- Spec - <https://download.eclipse.org/microprofile/microprofile-rest-client-2.0/microprofile-rest-client-spec-2.0.html#_responseexceptionmapper>
- Issue that tipped me off about this feature - <https://github.com/quarkusio/quarkus/issues/17153>
- Nice worked example - <https://itnext.io/how-to-deal-with-4xx-5xx-responses-in-microprofile-rest-client-2e16559f542>
- And even in Quarkus Rest client reactive exception handling - <https://quarkus.io/guides/rest-client-reactive#exception-handling>

```java
@Path("/api/test")
@RegisterRestClient(configKey = "api-call")
@RegisterProvider(CustomResponseExceptionMapper.class)
@ApplicationScoped
public interface SomeService {

  @POST
  @Consumes(MediaType.APPLICATION_JSON)
  @Produces(MediaType.APPLICATION_JSON)
  CompletionStage<Response> someServiceCall(@HeaderParam("some-header-name") String someHeader,
      SomeRequest someRequest);
}
```

```java
public class CustomResponseExceptionMapper implements ResponseExceptionMapper<WebApplicationException> {

  public WebApplicationException toThrowable(Response response) {
    if (response.getStatus() == 500) {
      Object errorCodeHeader = response.getHeaders().get(0);
      Object errorMsgHeader = response.getHeaders().get(1);

      if (errorCodeHeader != null && errorMsgHeader != null) {
        log.error("Error response: {} - {}", errorCodeHeader, errorMsgHeader);
      }
    }

    return new WebApplicationException("Service error, status code " + response.getStatus(), response);
  }
}

```

## Scheduling stuff in Quarkus

Can use standard Quarkus schedule or an actual Quarkus-Quartz Scheduler library which seems more fully featured

- Quartz - <https://quarkus.io/guides/quartz>
- Quarkus Scheduler - <https://quarkus.io/guides/scheduler>

```xml
<!-- Update for pom.xml -->
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-scheduler</artifactId>
</dependency>
```

```java
@ApplicationScoped              
public class SomeBean {

    
    @Scheduled(every="10s")     
    void doStuff() {...}

    @Scheduled(cron="0 15 10 * * ?") 
    void doStuff() {...}

    // Cron in the application config
    @Scheduled(cron = "{cron.expr}") 
    void doStuff() {...}
}
```

## Remote debug in Quarkus

- <https://access.redhat.com/documentation/en-us/red_hat_build_of_quarkus/1.3/html/developing_and_compiling_your_quarkus_applications_with_apache_maven/proc-debugging-your-quarkus-project_quarkus-maven>
- <https://blog.sebastian-daschner.com/entries/quarkus-remote-dev-in-containers-update>
- <https://gist.github.com/philipz/734b7e7595a8a3702f937a30ad5c5d81>
- <https://stackoverflow.com/questions/55190015/how-can-i-debug-my-quarkus-application-that-is-running-in-dev-mode>

```bash
# In local 
mvn quarkus:dev

# in remote container for example
mvn quarkus:remote-dev -Ddebug=false \
  -Dquarkus.package.type=mutable-jar \
  -Dquarkus.live-reload.url=http://localhost:8080 \
  -Dquarkus.live-reload.password=123

```

## Quarkus Testing

- Change config via test profiles - <https://quarkus.io/blog/quarkus-test-profiles/>
  - Implement an interface to provide a map of overridden properties

```java
@QuarkusTest
@TestProfile(SomeQuarkusTest.MyTestProfile.class)
class SomeQuarkusTest {

  public static class MyTestProfile implements QuarkusTestProfile {
    @Override
    public Map<String, String> getConfigOverrides() {
      return Map.of("someproperty.value", "true",
          "someservice.url", "http://localhost:9001/mockService");
    }
  }
```

- This works even from a Quarkus TestResource (when defining your own impl of the resource lifecycle manager) but without a test profile, the regular profile doesn't get access to the config params - maybe a lifecycle issue with instantiation.
