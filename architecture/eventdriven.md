# Event Driven Architecture

- [Event Driven Architecture](#event-driven-architecture)
  - [Articles Review](#articles-review)
    - [Sidecar and DAPR](#sidecar-and-dapr)
      - [Sidecar](#sidecar)
      - [DAPR](#dapr)
    - [Traditional architectures versus Reactive Microservices](#traditional-architectures-versus-reactive-microservices)
      - [Notes](#notes)
    - [Reactive message concepts - Smallrye Reactive Messaging Framework](#reactive-message-concepts---smallrye-reactive-messaging-framework)
      - [Microprofile Reactive Messaging Specification](#microprofile-reactive-messaging-specification)
    - [Service Oriented Architecture](#service-oriented-architecture)
  - [Technologies](#technologies)

- Describing event driven APIs <https://www.asyncapi.com/>

## Articles Review

### Sidecar and DAPR

- <https://docs.microsoft.com/en-us/azure/architecture/patterns/sidecar>
- <https://github.com/dapr/dapr>
- <https://dapr.io>

#### Sidecar

Paraphrased from Microsoft article:

> This pattern is named Sidecar because it resembles a sidecar attached to a motorcycle.
> In the pattern, the sidecar is attached to a parent application and provides supporting features for the application.
> Same lifecycle as the parent application, created/destroyed with parent.
> The sidecar pattern is sometimes referred to as the sidekick pattern and is a decomposition pattern.

- Separate core functionality from supporting services 
  - e.g. Logging
  - Allows heterogeneous environments.
  - Reduces dependencies on critical components - e.g. don't break app because logging stops working.
  - Access to same resources.
  - Can deploy independently.
  - Can control its resource utilization.

Example: Offload proxy. Place an NGINX proxy in front of a node.js service

Example: Infrastructure API - application can access logging, env data, config, health checks through the sidecar service.

#### DAPR

Dapr is a portable, serverless, event-driven runtime that makes it easy for developers to build resilient, stateless and stateful microservices that run on the cloud and edge and embraces the diversity of languages and developer frameworks.

Dapr injects a side-car (container or process) to each compute unit. The side-car interacts with event triggers and communicates with the compute unit via standard HTTP or gRPC protocols. This enables Dapr to support all existing and future programming languages without requiring you to import frameworks or libraries.

### Traditional architectures versus Reactive Microservices

- Article <https://developer.lightbend.com/docs/introduction/traditional-architecture.html>
  - See also martin fowler microservices - <https://martinfowler.com/articles/microservices.html#footnote-etymology>
    - Def of Microservice architectural style:  
      - microservice architectural style [1] is an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms, often an HTTP resource API. These services are built around business capabilities and independently deployable by fully automated deployment machinery. There is a bare minimum of centralized management of these services, which may be written in different programming languages and use different data storage technologies.
    - Def of Microservice: 
      - Independently deployable service with a single clearly scoped purpose or capability.
      - Cloud native, scalable, platform independent, decoupled and isolated, autonomous, devops continuous integration & deployment.

- Eclipse Microprofile is a group of API specifications for reactive microservices - basically what JEE architecture is for standard java applications, microprofile is for microservices/cloud - <https://microprofile.io/>.
  - SmallRye implements some of the APIs - e.g. reactive messaging

#### Notes

- Reactive principles (NB - Reactive manifesto - <https://www.reactivemanifesto.org/>)
  - Responsive, resilient, elastic, message driven
  - Reactive Microservices have following characteristics
    - Isolation (decoupled lifecycle, no impact to others in the system)
    - Autonomy (acts independently, own api of behaviour)
    - Single Responsibility
    - Event driven
    - Mobility (can be moved but reached in same way no matter its location)
    - Owns its own state.

- Event Sourcing
  - Possibilities to create event logs and to capture events not possible with a traditional storage - e.g. tracking events of products added and then removed from a cart
    - Adds complexity though - need to have a way to regroup these - e.g. splunk

### Reactive message concepts - Smallrye Reactive Messaging Framework

- from SmallRye Reactive Messaging - Concepts - <https://smallrye.io/smallrye-reactive-messaging/smallrye-reactive-messaging/3.9/concepts.html>

- `Messages` - message is an envelope around a payload. 
  - Applications work on messages and they can consume or produce them. 
  - They can be sent to/obtained from message brokers (e.g. Kafka). 
  - In Reactive Messaging the class is Message<T> and the payload is <T> e.g. String or some class.
  - In addition to Payload, can also have Metadata (e.g. Kafka MetaData, tracing data or even business related data)
- Channels
  - Messages transmit on a channel - a virtual destination identified by a name.
    - Stream is a structure of channels for component to read from and write to.
- Connectors
  - How your application interacts with the message brokers/event backbone. 
  - Connector connects to the broker and receives messages for the app, transmits to the broker on the specific channels for those functions.
  - Connector is tech specific e.g. Kafka broker.
  - Can work without connectors but must provide the message chain yourself - e.g. an @incoming method and @outgoing method.

TODO - Smallrye is definitely used with Kafka in Quarkus but is it also with NATS ? Not directly currently (from their website) but through Camel but this brings its own limitations... (aka our experience)

#### Microprofile Reactive Messaging Specification

- <https://download.eclipse.org/microprofile/microprofile-reactive-messaging-1.0/microprofile-reactive-messaging-spec.pdf>
  - 

### Service Oriented Architecture

- Article Notes on - <https://en.wikipedia.org/wiki/Service-oriented_architecture>

`Definition:`

> SOA (service-oriented architecture) is an architectural style that focus on discrete services instead of a monolithic design.

- Service is a discrete unit of functionality that can be accessed remotely and acted upon and updated independently
  - e.g Retrieving a credit card statement online, retrieving an order etc.

- Example properties that a service can have
  - Logically represents a repeatable business activity with a specified outcome.
  - Self-contained.
  - Black box for consumers - i.e. not aware of inner workings/implementation.
  - Can be composed of other services.

- Service Mesh
  - Using different services in conjunction to provide functionality for a large application
    - E.g. separately distributed, maintained and deployed software components. Enabled by network communication e.g. IP network.

- SOA vs API
  - API is the service, SOA is the architecture that allows the service to operate.

## Technologies

- `Microprofile` - <https://projects.eclipse.org/projects/technology.microprofile> - Equivalent of JEE for microservices architecture.
