# Cloud

- [Cloud](#cloud)
  - [Cloud definitions](#cloud-definitions)
    - [Characteristics](#characteristics)
    - [Service Models](#service-models)
    - [Deployment Models](#deployment-models)
    - [Regions, AZ](#regions-az)
    - [Kubernetes](#kubernetes)
    - [Microservice](#microservice)
    - [Service Mesh](#service-mesh)
    - [Monitoring and Alerting](#monitoring-and-alerting)
    - [Logging](#logging)
  - [Microservices](#microservices)

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

### Kubernetes

- Containers grouped in pods, deployed on nodes (physical servers) within a cluster.
- Kubernetes has solutions for shared volumes between containers (TODO - investigate this) and other shared and mirrored data sources when working with stateful microservices.

### Microservice

- Independently deployable service with a single clearly scoped purpose or capability.
  - Cloud native, scalable, platform independent, decoupled and isolated, autonomous, devops continuous integration & deployment.
  
### Service Mesh

- Network of microservices making up an application.
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