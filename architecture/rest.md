# REST JSON and Webservices

- [REST JSON and Webservices](#rest-json-and-webservices)
  - [General REST](#general-rest)
  - [Examples of good APIs](#examples-of-good-apis)
  - [Swagger](#swagger)
    - [Specifications](#specifications)
  - [YAML](#yaml)
  - [Rest Topics to learn about](#rest-topics-to-learn-about)
  - [Handling JSON](#handling-json)

- HTTP 1.1 vs 2 - <https://www.digitalocean.com/community/tutorials/http-1-1-vs-http-2-what-s-the-difference>

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

## Handling JSON

- Deserializing non-standard JSON fields (e.g. snake case naming) <https://www.baeldung.com/jackson-deserialize-snake-to-camel-case>
  - Many options but some examples
    - Annotations - @JsonProperty on fields, @JsonNaming(PropertyNamingStrategies.SnakeCaseStrategy.class) for class level (NB- many types of strategies)
    - A little gotcha in Quarkus, there can be conflicts if mixing the resteasy jsonb and jackson dependencies resulting in the JsonProperty annotations being ignored. Solution is to use jackson ones with the JsonProperty stuff for my case but it seems like jsonb properties could be more standard.

From stackoverflow: <https://stackoverflow.com/a/64101349>

```pre
 Your pom.xml include quarkus-rest-client and quarkus-resteasy-jsonb, I think these will trigger the use of JSONB for the rest client. I suggest to use quarkus-resteasy-jackson instead. You cannot use a different serialization layer for your REST endpoint and the REST client.
```

And here something about JSONB - <https://rieckpil.de/whatis-json-binding-json-b/>
