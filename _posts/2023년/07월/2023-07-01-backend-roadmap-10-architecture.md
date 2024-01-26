---
title: "[Roadmap] Backend Developer Roadmap: 10. Architectural Patterns"
excerpt: "백엔드 개발자 로드맵 분석 - Architectural Patterns에 대하여"
date: 2023-7-1
last_modified_at: 2023-7-1
categories:
  - essay
tags:
  - roadmap
  - backend
  - architecture
---

|Backend Roadmap|Link|
|:---|:---:|
|0. Roadmap|[Roadmap](https://roadmap.sh/backend)|
|1. Internet|[Internet](https://burningfalls.github.io/essay/backend-roadmap-1-internet/)|
|2. OS|[Operating System](https://burningfalls.github.io/essay/backend-roadmap-2-os/)|
|3. R-DB|[Relational Database](https://burningfalls.github.io/essay/backend-roadmap-3-relational-database/)|
|4. API|[API](https://burningfalls.github.io/essay/backend-roadmap-4-api/)|
|5. Caching|[Caching](https://burningfalls.github.io/essay/backend-roadmap-5-caching/)|
|6. Security|[Web Security](https://burningfalls.github.io/essay/backend-roadmap-6-web-security/)|
|7. Testing|[Testing](https://burningfalls.github.io/essay/backend-roadmap-7-testing/)|
|8. CI/CD|[CI/CD](https://burningfalls.github.io/essay/backend-roadmap-8-ci-cd/)|
|9. Design|[Design and Development Principles](https://burningfalls.github.io/essay/backend-roadmap-9-design/)|
|10. Architecture|[Architectural Patterns](https://burningfalls.github.io/essay/backend-roadmap-10-architecture/)|
|11. Search Engines|[Search Engines](https://burningfalls.github.io/essay/backend-roadmap-11-search-engines/)|
|12. OAuth|[OAuth](https://burningfalls.github.io/essay/backend-roadmap-12-oauth/)|
|13. Docker/K8s|[Docker and Kubernetes](https://burningfalls.github.io/essay/backend-roadmap-13-docker-and-k8s/)|

## 0. Architectural Patterns

`Architectural Pattern`은 **주어진 컨텍스트(context) 내 소프트웨어 아키텍처에서 일반적으로 발생하는 문제에 대한, 일반적이고 재사용 가능한 솔루션**이다. 아키텍처 패턴은 컴퓨터 하드웨어 성능 제한, 고가용성 및 비즈니스 위험 최소화와 같은 **소프트웨어 엔지니어링의 다양한 문제를 해결한다.**

## 1. Monolithic Apps

`Monolithic architecture`는 애플리케이션이 요청을 처리하고, 비즈니스 로직을 실행하고, 데이터베이스와 상호 작용하고, front-end용 HTML을 생성하는 패턴이다. 간단히 말해서, 이 **하나의 애플리케이션은 많은 일을 한다. 내부 구성 요소는 고도로 결합되어, 하나의 단위로 배치된다.**

## 2. Microservices

`Microservice architecture`는 응집력이 높고 느슨하게 결합된 서비스가 개별적으로 개발과 유지 관리 및 배포되는 패턴이다. **각 구성 요소는 개별 기능을 처리하고, 결합되면 애플리케이션이 전체 비즈니스 기능을 처리한다.**

## 3. SOA(service-oriented)

`Service-Oriented Architecture(SOA)`는 **서비스 인터페이스를 통해, 소프트웨어 구성 요소를 재사용할 수 있도록 하는 방법을 정의한다.** 이러한 인터페이스는 매번 심층 통합을 수행하지 않고도 새로운 애플리케이션에 신속하게 통합할 수 있는 방식으로 공통 통신 표준을 사용한다. 

## 4. Serverless

`Serverless`는 **개발자가 서버를 provisioning(사용자의 요구에 맞게 시스템 자원을 할당, 배치, 배포해 두었다가 필요 시 시스템을 즉시 사용할 수 있는 상태로 미리 준비해 두는 것)하거나 관리하지 않고, 애플리케이션을 빌드하고 실행하는 아키텍처이다.** 클라우드 컴퓨팅/서버리스에서는 서버가 존재하지만, 클라우드 공급자가 관리한다. 리소스는 필요에 따라 사용되며, 종종 Auto Scaling을 사용한다.

## 5. Service Mash

`Service Mash`는 **상호 연결된 지능형 proxy mesh를 사용하여 연결된 마이크로서비스 네트워크이다.** 마이크로서비스 간의 통신을 관리하고 보호하는 데 사용되며, 로드 밸런싱(load balancing), 서비스 검색 및 관찰 가능성(observability)과 같은 기능을 제공한다.

Service Mash에서 각 마이크로서비스는 일반적으로 "envoy"라고 하는 가볍고 투명한 proxy의 인스턴스(instance)로 표현된다. Envoy는 마이크로서비스 간의 통신을 처리하고, 로드 밸런싱, 라우팅 및 보안과 같은 기능을 제공한다.

Service Mesh는 일반적으로 사이드카(sidecar) 패턴을 사용하여 구현되며, 여기에서 메신저는 담당하는 마이크로서비스와 함께 배포된다. 이를 통해, Service Mesh를 마이크로서비스에서 분리할 수 있으며, 관리 및 업데이트가 더 쉬워진다.

Service Mesh는 일반적으로 클라우드 네이티브 아키텍처에서 사용되며, envoy 구성 및 관리를 담당하는 control plane을 사용하여 관리되는 경우가 많다. 일부 인기 있는 Service Mesh 구현에는 Istio와 Linkerd가 포함된다.

## 6. Twelve-Factor Apps

`Twelve-Factor App`은 **확장 가능하고 유지 관리 가능한 SaaS(Softwoare-as-a-Service) 애플리케이션을 구축하기 위한 방법론**이다. 방법론 작성자가 최신 클라우드 네이티브 애플리케이션을 구축하는 데 필수적인 것으로 식별한 일련의 모범 사례를 기반으로 한다.

Twelve-Factor App 방법론은 다음 원칙으로 구성된다:

* Codebase: 여러 배포가 포함된 애플리케이션에 대한 단일 코드베이스(codebase)가 있어야 한다.
* Dependencies: 애플리케이션은 해당 종속성(dependency)을 명시적으로 선언하고 분리해야 한다.
* Config: 애플리케이션은 환경에 구성(configuration)을 저장해야 한다.
* Backing services: 애플리케이션은 지원 서비스(backing service)를 연결된 리소스로 취급해야 한다.
* Build, release, run: 애플리케이션은 격리된 단위로 빌드(build), 릴리스(release) 및 실행(run)되어야 한다.
* Processes: 애플리케이션은 하나 이상의 상태비저장(stateless) 프로세스(process)로 실행되어야 한다.
* Port binding: 애플리케이션은 포트 바인딩(port binding)을 통해 서비스를 노출해야 한다.
* Concurrency: 응용 프로그램은 스레드(thread)를 추가하는 것이 아니라, 더 많은 프로세스를 추가하여 확장해야 한다.
* Disposability: 응용 프로그램은 빠르게 시작하고 중지하도록 설계되어야 한다.
* Dev/prod parity: 개발(dev:develoopment), 스테이징(staging) 및 프로덕션(prod:production) 환경은 최대한 유사해야 한다.
* Logs: 애플리케이션은 로그(log)를 event stream으로 처리해야 한다.
* Admin processes: 애플리케이션은 관리/유지관리(admin/maintenance) 작업을 일회성(one-off) 프로세스로 실행해야 한다.

Twelve-Factor App 방법론은 SaaS 애플리케이션 개발자가 널리 채택하고 있으며, 확장 가능하고 유지 관리가 가능하며 배포하기 쉬운 클라우드 네이티브 애플리케이션을 구축하기 위한 모범 사례로 간주된다.

## 7. References

[Architectural Patterns](https://roadmap.sh/backend)