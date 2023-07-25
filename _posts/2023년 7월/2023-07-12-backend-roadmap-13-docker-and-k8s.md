---
title: "[Roadmap] Backend Developer Roadmap: 13. Docker and Kubernetes"
excerpt: "백엔드 개발자 로드맵 분석 - Docker와 Kubernetes에 대하여"
date: 2023-7-12
last_modified_at: 2023-7-12
categories:
  - essay
tags:
  - roadmap
  - backend
  - docker
  - kubernetes
---

|Backend Roadmap|Link|
|:---|:---:|
|0. Roadmap|[Roadmap](https://roadmap.sh/backend)|
|1. Internet|[Internet](https://burningfalls.github.io/essay/backend-roadmap-1-internet/)|
|2. OS|[Operating System](https://burningfalls.github.io/essay/backend-roadmap-2-os/)|
|3. R-DB|[Relational Database](https://burningfalls.github.io/essay/backend-roadmap-3-relational-database/)|
|4. API|[API](https://burningfalls.github.io/essay/backend-roadmap-4-api/)|
|5. Caching|[Caching](https://burningfalls.github.io/essay/backend-roadmap-5-caching/)|
|6. Security|[Web Security](https://burningfalls.github.io/essay/backend-roadmap-6-caching/)|
|7. Testing|[Testing](https://burningfalls.github.io/essay/backend-roadmap-7-testing/)|
|8. CI/CD|[CI/CD](https://burningfalls.github.io/essay/backend-roadmap-8-ci-cd/)|
|9. Design|[Design and Development Principles](https://burningfalls.github.io/essay/backend-roadmap-9-design/)|
|10. Architecture|[Architectural Patterns](https://burningfalls.github.io/essay/backend-roadmap-10-architecture/)|
|11. Search Engines|[Search Engines](https://burningfalls.github.io/essay/backend-roadmap-11-search-engines/)|
|12. OAuth|[OAuth](https://burningfalls.github.io/essay/backend-roadmap-12-oauth/)|
|13. Docker/K8s|[Docker and Kubernetes](https://burningfalls.github.io/essay/backend-roadmap-13-docker-and-k8s/)|

## Docker

### 1. What is Docker?

`Docker` is a conatiner technology: A tool for creating and managing containers

`Container`
  - A standardized unit of software
  - A package of code and dependencies to run that code (e.g. NodeJS code + the NodeJS runtime)
  - The same container always yields the exact same application and execution behavior. No matter where or by whom it might be executed.
  - Support for Containers is build into modern operating systems.
  - Docker simplifies the creation and management of such containers

### 2. Why Containers?

We want reliability and reproducible environments

- We want to have the **exact same environment for development and production** -> this ensures that is works exactly as tested
- It should be easy to **share a common development environment** or setup with (new) employees and colleagues
- We **don't want to uninstall and re-install** local dependencies and runtimes all the time

### 3. Virtual Machines vs Docker Containers

|Docker Containers||Virtual Machines|
|:--:||:--:|
|Low impac on OS, very fast, minimal disk space usage||Bigger impact on OS, slower, higher disk spaces uage|
|Sharing, re-building and distribution is easy||Sharing, re-building and distribution can be challenging|
|Encapsulate apps/ environments instead of "whole machines"||Encapsulate "whole machines" instead of just apps/ environments|

## Kubernetes

### 1. Problem and Solve(AWS ECS)

Manual deployment of Containers is hard  to maintain, error-prone and annoying (ene beyond security and configuration concerns)

- Containers might crash or go down and need to be replaced -> Container health checks + automatic re-deployment
- We might need more container instances upon traffic spikes -> Autoscaling
- Incoming traffic should be distributed equally -> Load balancer

### 2. Further Problem

Using a specific cloud service locks us into that service.

You need to learn about the specifics, services and config options of another provider if you want to switch.

Just knowing Docker isn't enough.

### 3. Kubernetes

`Kubernetes`: An open-source system (and de-facto standard) for orchestrating container deployments

* Automatic Deployment
* Scaling & Load Balancing
* Management

### 4. Why Kubernetes?

* Using with Any Cloud Provider or Remote Machines (Kubernetes Configuration)

* Extensible, yet standardized configuration: Standardized way of describing the to-be-created and to-be-managed resources of the Kubernetes Cluster (Cloud-provider-specific settings can be added)

### 5. What Kubernetes IS and IS NOT

* It's not a cloud service provider -> It's an open-source project
* It's not a service by a cloud service provider -> It can be used with any provider
* It's not restricted to any specific (cloud) service provider -> It can be used with any provider
* It's not just a software you run on some machine -> It's a collection of concepts and tools
* It's not an alternative to Docker -> It works with (Docker) containers
* It's not a paid service -> It's a free open-source project

Therefore, Kubernetes is like Docker-Compose for multiple machines