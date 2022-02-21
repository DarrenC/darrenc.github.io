# Cloud

- [Cloud](#cloud)
  - [Cloud definitions](#cloud-definitions)
    - [Characteristics](#characteristics)
    - [Service Models](#service-models)
    - [Deployment Models](#deployment-models)
    - [Regions, AZ](#regions-az)
    - [Cloud Native](#cloud-native)
    - [Kubernetes](#kubernetes)
    - [Microservice](#microservice)
    - [Service Mesh](#service-mesh)
    - [Monitoring and Alerting](#monitoring-and-alerting)
    - [Logging](#logging)
  - [Microservices](#microservices)
  - [Messaging - Kafka](#messaging---kafka)
    - [Use Cases](#use-cases)
    - [Kafka APIs](#kafka-apis)
    - [Semantics](#semantics)
    - [Components](#components)
    - [KEY CONCEPT - Topics and Partitions](#key-concept---topics-and-partitions)
    - [Kafka Performance points](#kafka-performance-points)
  - [NATS](#nats)

## Cloud definitions

### Characteristics

- On-Demand services
- Shared Resource pooling
- Online access
- Elasticity: flexibility of resources
- Measured/Metered services

### Service Models

- IaaS: Infrastructure as a service - configure infrastructure to run applications
- PaaS: Platform as a service - platform is a machine with OS - e.g. a linux box
- SaaS: Software as a service - gmail, Office365

Also:

- Daas: Desktop as a service
- Baas: Backend as a service (e.g. APIs to connect web/mobile clients to cloud services)
- DCaas: DataCentre as a service - rent data centre infrastructure

### Deployment Models

- Private Cloud: single org or company
- Public Cloud: shared with everyone
- Community Cloud: limited sharing between a group of orgs
- Hybrid Cloud: mix private and public cloud (good for security, choose which parts to share)

### Regions, AZ

- Availability Zone: unique physical location - i.e. one or more datacentres
- Region: group of AZ deployed with a defined latency perimeter, connected by low-latency network
- Geography: area of the world containing a discrete market containing one/more regions

### Cloud Native

- Definition (Cloud Native Computing Foundation)

```text

    Cloud-native technologies empower organizations to build and run scalable applications in modern, dynamic environments such as public, private, and hybrid clouds. Containers, service meshes, micro-services, immutable infrastructure, and declarative APIs exemplify this approach.

    These techniques enable loosely coupled systems that are resilient, manageable, and observable. Combined with robust automation, they allow engineers to make high-impact changes frequently and predictably with minimal toil.

```

- <https://docs.microsoft.com/en-us/dotnet/architecture/cloud-native/definition>

### Kubernetes

- Containers grouped in pods, deployed on nodes (physical servers) within a cluster.
- Kubernetes has solutions for shared volumes between containers (TODO - investigate this) and other shared and mirrored data sources when working with stateful micro-services.
- [Kubernetes and Helm](./kubernetes_helm.md)

### Microservice

- Independently deployable service with a single clearly scoped purpose or capability.
  - Cloud native, scalable, platform independent, decoupled and isolated, autonomous, devops continuous integration & deployment.
  
### Service Mesh

- Network of micro-services making up an application.
- ISTIO, Linkerd are tools that handle this as complexity grows.

### Monitoring and Alerting

- Prometheus - monitoring and alerting
- Grafana/Kibana - data visualization
- Fluentd - data gathering
- Kafka - messaging - Overview of Kafka <https://medium.com/swlh/apache-kafka-in-a-nutshell-5782b01d9ffb>

### Logging

- Splunk
- Elastic search
- ELK - elastic search, logstash, kibana

## Microservices

<https://martinfowler.com/articles/microservices.html>

> The term "Microservice Architecture" has sprung up over the last few years to describe a particular way of designing software applications as suites of independently deployable services. While there is no precise definition of this architectural style, there are certain common characteristics around organization around business capability, automated deployment, intelligence in the endpoints, and decentralized control of languages and data.

## Messaging - Kafka

TODO -> need a page just for this I think

### Use Cases

- Publish-Subscribe
- Log Shipping
- Log Aggregation
- Staged Event-Driven Architecture (SEDA)
- Complex Event Processing (CEP)
- Event sourced Command-Query Responsibility Segregation (CQRS)

### Kafka APIs

- Producer API
  - Writing stuff to topics
- Consumer API
  - Consuming stuff from topics
- Streams API
  - Transforming stuff from a Producer and then making it available to Consumers
- Connector API
  - Reusing connections e.g. MongoDB connector to share them with other developers

### Semantics

- At least once
- At most once
- (exactly once)

### Components

- Producer
- Consumer
- Broker
  - Handle the IO and operations. 
  - One broker is the controller - manages partition states
  - partitions can be replicated on multiple brokers
- Zookeeper
  - Handle the overall operations - heartbeats, controller election etc., config repository, quotas, user ACL
  - must be odd number due to underlying protocols

### KEY CONCEPT - Topics and Partitions

- Topic
  - Logical regrouping of partitions
  - Partition belongs to exactly one partition
- Partition
  - Totally ordered sequence of records
    - record has offset and may have key & value
    - Multiple Producers may publish records to a partition but the order is always respected (but really publish to a topic)
    - There is no order across Producers though
  - Within a topic, partitions are independent - i.e. PARTIALLY ORDERED with respect to the topic
  - Allows processing in parallel where possible, in order where necessary
  - Producers give records the same key to indicate they should be on the same partition (kafka hashes the key to calc partition). With different keys they may be on different partitions
- Consumers subscribe to a topic as part of a consumer group
  - First consumer gets all the partitions
  - Second consumer arrives and takes half and so on.....
  - Partition is never assigned to multiple consumers (if more consumers than partitions, idle consumers)
- Consuming record does not delete
  - Topic is an append only ledger
  - Kafka (or Producer) is the only one to modify
  - Consumer maintains an offset - points to next record
  - New consumer joining the topic starts by processing from the last committed offset
  - Default - consumer commits offset to cluster every 5 seconds
    - enable.auto.commit can be modified to false - allows to control when the commit happens
      - move from at most once reads to at least once - delivery guarantees (if crash during processing, record can be reprocessed)
  - Multiple consumer groups can subscribe to topics + work independently of each other.
    - Each gets individual partition assignments and offsets.

### Kafka Performance points

- Kafka is optimised for throughput
  - Speed from using append-only logs, largely constrained to sequential I/O
  - Multiple records can be batched - increases performance especially with compression
  - Batching usually client-side operation - load on client, reduces network bandwidth utilisation.
    - client handles key-hash, checksum, alignment in the consumer’s staging accumulator 
    - Broker mostly just dumps them straight to disk upon receipt.
  - Offsets in Kafka
    - Key difference with MQ-Style brokers since the message removal is no longer at point of consumption (avoid random IO penalty)
    - consumer offsets to track it - append only to be fast
  - Consumers in Kafka are cheap - can have many concurrently without perf issues
  - Fsync not called
    - Another fundamental reason for Kafka’s performance, and one that is a lesser-known fact: Kafka doesn’t actually call fsync when writing to the disk before acknowledging the write; the only requirement for an ACK is that the record has been written to the I/O buffer. This is, in fact, what actually makes Kafka perform as if it were an in-memory queue — because for all intents and purposes it is a disk-backed in-memory queue (limited by the size of the buffer/pagecache).

BUT THERE ARE DRAWBACKS

- Latency
  - Optimised almost exclusively for throughput, Kafka is not what you might comfortably call a ‘low latency’ messaging platform.
  - End-to-end latencies can reach into the tens or hundreds of milliseconds.
  - Not comparable to dedicated low-latency solutions, which can comfortably operate in the sub-microsecond range.
  - Don’t use it in applications like high-frequency trading, where low, predictable latency is a must.
  - Unsafe defaults. Kafka authors make several bold claims around the strength of their ordering and delivery guarantees. You would then be forgiven for assuming that the defaults are sensible, insofar as they ought to favour safety over other competing qualities. Kafka defaults tend to be optimised for performance and will need to be explicitly overridden on the client when safety is a critical objective. Some of the specific gotchas to bear in mind:
  - enable.auto.commit — defaults to true, which results in consumers committing offsets every 5 seconds (configured by auto.commit.interval.ms), irrespective of whether the consumer has finished processing the record. This may lead to mixed delivery semantics — in the event of consumer failure, some records might be delivered twice, while others might not be delivered at all. Set this to false, allowing your application to dictate the commit point.
    max.in.flight.requests.per.connection — defaults to 5, which may result in messages being published out-of-order if one (or more) of the enqueued messages times out and is retried. Set to 1.

## NATS

- <https://medium.com/capital-one-tech/lightweight-cloud-native-messaging-with-nats-ad730ca2becf>
- <https://docs.nats.io/nats-concepts/jetstream>