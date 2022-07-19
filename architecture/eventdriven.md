# Event Driven Architecture

- [Event Driven Architecture](#event-driven-architecture)
  - [Articles Review](#articles-review)
    - [Sidecar and DAPR](#sidecar-and-dapr)
      - [Sidecar](#sidecar)
      - [DAPR](#dapr)
    - [Traditional architectures versus Reactive Microservices](#traditional-architectures-versus-reactive-microservices)
      - [Notes](#notes)

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
