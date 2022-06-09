# Event Driven Architecture

- [Event Driven Architecture](#event-driven-architecture)
  - [Articles Review](#articles-review)
    - [Sidecar and DAPR](#sidecar-and-dapr)
      - [Sidecar](#sidecar)
      - [DAPR](#dapr)

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