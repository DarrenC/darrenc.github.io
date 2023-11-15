# REST JSON and Webservices

- [REST JSON and Webservices](#rest-json-and-webservices)
  - [General REST](#general-rest)
    - [HTTP Authentication Schemes and HTTP Authorization header](#http-authentication-schemes-and-http-authorization-header)
  - [Examples of good APIs](#examples-of-good-apis)
  - [Swagger](#swagger)
    - [Specifications](#specifications)
  - [YAML](#yaml)
  - [Rest Topics to learn about](#rest-topics-to-learn-about)
  - [Handling JSON with Jackson](#handling-json-with-jackson)
    - [Deserializing non-standard case JSON fields](#deserializing-non-standard-case-json-fields)
    - [Handling missing or unknown JSON fields](#handling-missing-or-unknown-json-fields)
    - [Ignoring certain fields to not map them](#ignoring-certain-fields-to-not-map-them)
  - [API Design Patterns book](#api-design-patterns-book)
    - [Part 2 Design Principles](#part-2-design-principles)
      - [Chapter 3 - Naming](#chapter-3---naming)

## General REST

- <https://mickadoo.github.io/rest/2016/09/26/what-is-rest.html> - v.
    nice
- discussion on reddit -
    <https://www.reddit.com/r/rest/comments/54nnoo/trying_to_understand_the_fielding_dissertation/>
- <http://stackoverflow.com/questions/671118/what-exactly-is-restful-programming>
- <http://getmesh.io/Blog/REST+in+Peace+-+Devoxx+Poland+2016>
- <http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven>
- <http://web.archive.org/web/20130116005443/http://tomayko.com/writings/rest-to-my-wife>
- <http://www.ics.uci.edu/~fielding/pubs/dissertation/fielding_dissertation.pdf>
- Rest API guidelines Zalando -
    <https://opensource.zalando.com/restful-api-guidelines/#introduction>

### HTTP Authentication Schemes and HTTP Authorization header

You can get authorization to request a resource by providing an authorization header with a authentication string. 
This might be a multi-step approach - send an authorization header with an encoded user/pass and get an access token to send in subsequent requests in the same authorization header.
Typically Basic and Bearer for the types of request as the value of the authorization header.

- Details <https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#authentication_schemes>
  - Basic - (RFC 7617), base64-encoded credentials - i.e. encoded string with form user:password - 200 OK if successful
    - Can be a specific authentication resource and might give back a token (see next point)
    - Base64 can be simply decoded so only use with HTTPS and regard as not really secure.
  - Bearer - (RFC 6750), bearer tokens to access OAuth 2.0-protected resources - could be obtained from basic authentication request

## Examples of good APIs

What makes APIs success stories:

- Stripe
- Google Places
- Yelp
- Twitter
- Facebook Graph
- Uber
- Zalando

## Swagger

- <http://swagger.io/>
- <https://openapis.org/>
- <http://bigstickcarpet.com/swagger-parser/www/index.html#your-api-pane>
- <https://apihandyman.io/writing-openapi-swagger-specification-tutorial-part-6-defining-security/>
- OpenApi 3 tutorial -
    <https://idratherbewriting.com/learnapidoc/pubapis_openapi_tutorial_overview.html>

### Specifications

- Swagger 2 spec - <https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md>
- OpenAPI 3 spec - <https://github.com/OAI/OpenAPI-Specification>
  - <https://blog.stoplight.io/difference-between-open-v2-v3-v31>

## YAML

<http://www.yaml.org/start.html> YAML: YAML Ain\'t Markup Language

What It Is: YAML is a human friendly data serialization standard for all programming languages.

- Interesting article on Rest with Swagger -> talks about service first design
  - <https://blog.philipphauer.de/enriching-restful-services-swagger/>

## Rest Topics to learn about

- Resource
- Hateoas
- Versioning
- Controller
- Data model
- HTTP methods, header, status
- DNS URI
- AsyncAPI, Asynchronous REST
- Polymorphism & Data Dictionary
- Swagger & OpenAPI

## Handling JSON with Jackson

- Examples of Serializing/Deserializing: <https://stackabuse.com/definitive-guide-to-jackson-objectmapper-serialize-and-deserialize-java-objects/>

### Deserializing non-standard case JSON fields

- Deserializing non-standard JSON fields (e.g. snake case naming) <https://www.baeldung.com/jackson-deserialize-snake-to-camel-case>
  - Many options but some examples
    - Annotations - @JsonProperty on fields, @JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class) for class level (NB- many types of strategies)
    - A little gotcha in Quarkus, there can be conflicts if mixing the resteasy jsonb and jackson dependencies resulting in the JsonProperty annotations being ignored. Solution is to use jackson ones with the JsonProperty stuff for my case but it seems like jsonb properties could be more standard.

From stackoverflow: <https://stackoverflow.com/a/64101349>

```pre
 Your pom.xml include quarkus-rest-client and quarkus-resteasy-jsonb, I think these will trigger the use of JSONB for the rest client. I suggest to use quarkus-resteasy-jackson instead. You cannot use a different serialization layer for your REST endpoint and the REST client.
```

And here something about JSONB - <https://rieckpil.de/whatis-json-binding-json-b/>

### Handling missing or unknown JSON fields

- If an API changes or if we receive partial messages it can provoke errors when trying to read the response entities
  - e.g. UnrecognizedPropertyException
- Page describing different approaches <https://www.baeldung.com/jackson-deserialize-json-unknown-properties>

**Solution:**

- Configure ObjectMapper to IGNORE any unknown or missing properties

```java
  ObjectMapper mapper = new ObjectMapper()
    .configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
```

```bash
# Example of log for this issue
Caused by: com.fasterxml.jackson.databind.exc.UnrecognizedPropertyException: 
Unrecognized field "referenceId" (class com.me.MyClass), not marked as ignorable 
(3 known properties: "name", "address", "dob"])

```

### Ignoring certain fields to not map them 

- <https://www.baeldung.com/jackson-ignore-properties-on-serialization>
  - Can ignore fields by defining with annotation at class or field level in the code
  - Can ignore entire class with @JsonIgnoreType
    - Can even ignore classes we don't control with a Jackson MixIn and adding a mapping in the mapper
  - Can filter fields - <https://www.baeldung.com/jackson-ignore-properties-on-serialization#filters>

```java
public MyClass {

  private String name;
  // Ignore on a field
  @JsonIgnore
  private String internalInfo;
}

```

## API Design Patterns book

- <https://learning.oreilly.com/library/view/api-design-patterns/9781617295850/OEBPS/Text/ifc.xhtml>

### Part 2 Design Principles

#### Chapter 3 - Naming

- Updating a name is really expensive and difficult - worth spending time getting it right
  - PUBLIC face of your API
  - Very different to code where you can update quickly as understanding changes
  - Aim for
    - expressive - clearly conveys the thing it names
    - simple - not too long but not truncated either
    - predictable - be consistent - same name should be the same thing, different name should be a different thing


