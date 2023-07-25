---
title: "[Roadmap] Backend Developer Roadmap: 8. CI/CD"
excerpt: "백엔드 개발자 로드맵 분석 - CI/CD에 대하여"
date: 2023-6-29
last_modified_at: 2023-6-29
categories:
  - essay
tags:
  - roadmap
  - backend
  - ci-cd
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

## 0. What is CI/CD?

`CI(Continuous Integration)`/`CD(Continuous Delivery)`는 **문제를 조기에 감지하고 프로덕션 환경에 더 빠른 릴리스를 제공하는 것을 주요 목표로, 애플리케이션의 구축, 테스트 및 배포를 자동화하는 방법이다.**

## 1. CI/CD explained

**`CI/CD`는 `DevOps`(the joining of development and operations teams) 즉, 개발 팀과 운영 팀의 결합에 속하며, 지속적 통합(continuous integration)과 지속적 배포(continuous delivery)의 과정을 결합한다.** CI/CD는 infrastructure provisioning뿐만 아니라 빌드, 테스트(integration test, unit test, regression test) 및 배포 단계를 포함하여, 커밋에서 프로덕션으로 새 코드를 가져오는데 전통적으로 필요한 수동 인간 개입의 대부분 또는 전부를 자동화한다. CI/CD pipeline을 사용하여, 개발 팀은 코드를 변경한 다음, 전달 및 배포를 위해 자동으로 테스트되고 푸시된다. CI/CD를 올바르게 가져오면, 다운타임(downtime)이 최소화되고 코드 배포가 더 빨라진다.

CI/CD는 DevOps 및 최신 소프트웨어 개발 방식의 필수 부분이다. 특별히 제작된 CI/CD 플랫폼은 내장된 자동화와 테스트 및 협업을 통해 조직의 생산성을 개선하고 효율성을 높이며, 워크플로우를 간소화하여 개발 시간을 최대화할 수 있다. 애플리케이션이 커짐에 따라 CI/CD의 기능은 개발 복잡성을 줄이는데 도움이 될 수 있다. 다른 DevOps 방식(ex. 보안을 유지하고 더 긴밀한 피드백 루프 생성)을 채택하면, 조직이 개발 사일로(silos)를 허물고 안전하게 확장하며, CI/CD를 최대한 활용할 수 있다.

CI/CD는 개발, 보안 및 운영 팀이 최대한 효율적이고 효과적으로 작업하는 데 도움이 되기 때문에 중요하다. 지루하고 시간 소모적인 수동 개발 작업과 레거시(legacy) 승인 프로세스를 줄여, DevOps 팀이 소프트웨어 개발에서 보다 혁신적이 될 수 있도록 한다. 자동화는 프로세스를 예측 가능하고 반복 가능하게 만들어, 사람의 개입으로 인한 오류 가능성을 줄인다. DevOps 팀은 더 빠른 피드백을 얻고 더 작은 변경 사항을 자주 통합하여, 빌드 중단 변경의 위험을 줄일 수 있다. DevOps 프로세스를 지속적이고 반복적으로 만들면, 소프트웨어 개발 수명 주기가 단축되어, 조직에서 고객이 좋아하는 더 많은 기능을 제공할 수 있다.

## 1.1. What is continuous integration(CI)?

`Continuous Integration(CI)`는 **모든 코드 변경 사항을 공유 소스 코드 저장소의 기본 분기에 조기에 자주 통합하고, 각 변경 사항을 커밋하거나 병합할 때 자동으로 테스트하고 자동으로 빌드를 시작하는 방법이다.** continuous integration을 통해 오류 및 보안 문제를 식별하고, 보다 쉽게 그리고 개발 프로세스 초기에 수정할 수 있다.

변경 사항을 자주 병합하고 자동 테스트 및 유효성 검사 프로세스를 트리거(trigger)하면, 여러 개발자가 동일한 애플리케이션에서 작업하는 경우에도 코드 충돌 가능성을 최소화할 수 있다. 두 번째 장점은 답변을 오래 기다릴 필요가 없으며, 필요한 경우 주제가 아직 생생할 때 버그와 보안 문제를 수정할 수 있다는 것이다.

일반적인 코드 유효성 검사 프로세스는 코드 품질을 확인하는 정적 코드 분석으로 시작된다. 코드가 정적 테스트를 통과하면, 자동화된 CI 루틴이 추가 자동화 테스트를 위해 코드를 패키징(packaging)하고 컴파일(compile)한다. CI 프로세스에는 사용된 코드의 버전을 알 수 있도록 변경 사항을 추적하는 버전 제어 시스템이 있어야 한다.

### 1.2. What is continuous delivery(CD)?

`Continuous Delivery(CD)`는 **인프라 provisioning 및 애플리케이션 릴리스(release) 프로세스를 자동화하기 위해, CI와 함꼐 작동하는 소프트웨어 개발 방법이다.**

코드가 테스트되고 CI 프로세스의 일부로 빌드되면, CD는 최종 단계에서 인계받아 언제든지 모든 환경에 배포하는 데 필요한 모든 것을 패키징한다. CD는 인프라 provisioning에서 애플리케이션을 테스트 또는 프로덕션 환경에 배포하는 것까지 모든 것을 다룰 수 있다.

CD를 사용하면, 언제든지 프로덕션에 배포할 수 있도록 소프트웨어가 구축된다. 그런 다음 배포를 수동으로 트리거하거나 배포도 자동화되는 연속 배포로 이동할 수 있다.

### 1.3. What is continuous deployment?

`Continuous Deployment`를 통해 **조직은 응용 프로그램을 자동으로 배포**할 수 있으므로, 사람이 개입할 필요가 없다. continuous deployment를 통해 DevOps 팀은 미리 코드 릴리스 기준을 설정하고, 이러한 기준이 충족되고 검증되면 코드가 프로덕션 환경에 배포된다. 이를 통해 조직은 더 민첩해지고 새로운 기능을 사용자에게 더 빨리 제공할 수 있다.

continuous delivery 또는 deployment 없이 continuous integration을 수행할 수 있지만, CI가 있지 않으면 CD를 수행할 수 없다. 공유 저장소에 코드 통합, 테스트 및 빌드 자동화, 매일 작은 배치로 모든 작업을 수행하는 것과 같은 CI 기본 사항을 연습하지 않는 경우, 언제든지 프로덕션에 배포할 수 있기가 매우 어렵기 때문이다.

### 1.4. What is continuous testing?

`Continuous Testing`은 **버그가 코드베이스에 도입되는 즉시 식별하기 위해, 테스트가 지속적으로 실행되는 소프트웨어 테스트 방법**이다. CI/CD pipeline에서 continuous testing은 일반적으로 자동으로 수행되며, 각 코드 변경은 애플리케이션이 여전히 예상대로 작동하는지 확인하기 위해 일련의 테스트를 트리거한다. 이를 통해 개발 프로세스 초기에 문제를 식별하고, 나중에 수정하기가 더 어려워지고 비용이 많이 드는 것을 방지할 수 있다. continuous testing은 개발자에게 코드 품질에 대한 귀중한 피드백을 제공하여, 프로덕션에 출시되기 전에 잠재적인 문제를 식별하고 해결하는 데 도움이 될 수 있다.

연속 테스트에서는 CI/CD pipeline 내에서 다양한 유형의 테스트가 수행된다. 여기에는 다음이 포함될 수 있다.

* Unit testing: 개별 코드 단위가 예상대로 작동하는지 확인
* Integration testing: 응용 프로그램 내의 서로 다른 모듈 또는 서비스가 함께 작동하는 방식을 확인
* Regression testing: 특정 버그가 다시 발생하지 않도록 버그가 수정된 후 작동하는지 확인

## 2. CI/CD fundamentals

개발 수명 주기의 효율성을 극대화하는 데 도움이 되는 CI/CD의 8가지 기본 요소가 있다. 이들은 개발 및 배포에 걸쳐 있다. 다음 기본 사항을 pipeline에 포함하여, DevOps 워크플로우(workflow) 및 소프트웨어 제공을 개선할 수 있다.

(1) A single source repository

빌드를 생성하는 데 필요한 모든 파일과 스크립트를 포함하는 소스 코드 관리(Source code management: SCM)가 중요하다. **저장소에는 빌드에 필요한 모든 것이 포함되어야 한다.** 여기에는 소스 코드, 데이터베이스 구조, 라이브러리, 속성 파일 및 버전 제어가 포함된다. 또한, 애플리케이션을 빌드하기 위한 테스트 스크립트와 스크립트도 포함해야 한다.

(2) Frequent check-ins to main branch

trunk, mainline, master branch(trunk-based 개발)에 코드를 조기에 자주 통합한다. sub-branch를 피하고 main branch로만 작업한다. 작은 코드 세그먼트(segment)를 사용하고, **가능한 한 자주 main branch에 병합(merge)한다.** 한 번에 둘 이상의 변경 사항을 병합하지 않는다.

(3) Automated builds

스크립트에는 single command에서 빌드하는 데 필요한 모든 것이 포함되어야 한다. 여기에는 웹 서버 파일, 데이터베이스 스크립트 및 애플리케이션 소프트웨어가 포함된다. **CI 프로세스는 코드를 자도응로 패키징하고, 사용 가능한 애플리케이션으로 컴파일해야 한다.**

(4) Self-testing builds

**CI/CD는 지속적인 테스트가 필요하다.** 테스트 스크립트는 테스트 실패 시 빌드 실패로 이어지도록 해야 한다. 빌드 전 정적 테스트 스크립트를 사용하여 코드의 무결성, 품질 및 보안 규정 준수를 확인한다. 빌드에 정적 테스트를 전달하는 코드만 허용한다.

(5) Frequent iterations

저장소에 대한 여러 커밋으로 인해, 충돌(conflict)을 숨길 위치가 줄어든다. **대대적인 변경보다는 작고 자주 반복한다.** 이렇게 하면, 문제나 충돌이 있는 경우, 변경 사항을 쉽게 롤백할 수 있다.

(6) Stable testing environments

**코드는 프로덕션 환경의 복제된 버전에서 테스트해야 한다.** 라이브 프로덕션 버전에서는 새 코드를 테스트할 수 없다. 실제 환경에 최대한 가깝게 복제된 환경을 만든다. 엄격한 테스트 스크립트를 사용하여, 초기 빌드 전 테스트 프로세스를 통과하지 못한 버그를 감지하고 식별한다.

(7) Maximum visibility

**모든 개발자는 최신 실행 파일에 액세스하고 저장소에 대한 모든 변경 사항을 볼 수 있어야 한다.** 저장소의 정보는 모두에게 표시되어야 한다. 버전 제어를 사용하여 핸드오프(handoff)를 관리하여, 개발자가 최신 버전을 알 수 있도록 한다. 최대 가시성은 모든 사람이 진행 상황을 모니터링하고 잠재적인 문제를 식별할 수 있음을 의미한다.

(8) Predictable deployments anytime

배포는  팀이 언제든지 편안하게 수행할 수 있도록 일상적이고 위험이 낮아야 한다. **CI/CD 테스트 및 검증 프로세스는 엄격하고 신뢰할 수 있어야**, 팀이 언제든지 업데이트를 배포할 수 있다는 확신을 가질 수 있다. 제한된 변경 사항을 포함하는 빈번한 배포는, 또한 위험을 낮추고 쉽게 롤백할 수 있다.

## 3. The benefits of CI/CD implementation

CI/CD를 도입한 기업과 조직은 긍정적인 변화를 많이 체감하는 경향이 있다. 다음은 CI/CD를 구현할 때 기대할 수 있는 몇 가지 이점이다:

* Happier users and customers: 버그와 오류가 줄어들어 생산에 들어가므로, **사용자와 고객이 더 나은 경험을 할 수 있다.** 이를 통해 고객 만족도 수준이 향상되고, 고객 신뢰도가 향상되며, 조직에 대한 평판이 높아진다.
* Accelerated time-to-value: 언제든지 배포할 수 있으면, **제품과 새로운 기능을 더 빨리 시장에 출시할 수 있다.** 개발 비용이 낮아지고 처리 시간이 단축되어, 팀이 다른 작업을 할 수 있다. 고객은 결과를 더 빨리 얻을 수 있으므로, 회사는 경쟁 우위를 확보할 수 있다.
* Less fire fighting: 코드를 더 자주, 더 작은 배치로, 개발 주기 초기에 테스트하면 **fire drill을 크게 줄일 수 있다.** 그 결과, 개발 주기가 더 원활해지고 팀 스트레스가 줄어든다. 결과를 더 예측 가능하고 버그를 찾아 수정하기가 더 쉽다.
* Hit dates more reliably: 배포 병목 현상을 제거하고 배포를 예측 가능하게 만들면, **주요 날짜를 맞추는 것과 관련된 많은 불확실성을 제거**할 수 있다. 작업을 더 작고 관리하기 쉬운 단위로 나누면, 각 단계를 제시간에 완료하고 진행 상황을 추적하기가 더 쉬워진다. 이 접근 방식은 전체 진행 상황을 모니터링하고, 완료 날짜를 보다 정확하게 결정할 수 있는 충분한 시간을 제공한다.
* Free up developers' time: 더 많은 배포 프로세스가 자동화됨에 따라, **팀은 더 보람 있는 프로젝트를 위한 시간을 갖게 되었다.** 개발자는 시간의 35%~50%를 코드 테스트, 유효성 검사 및 디버깅에 사용하는 것으로 추정된다. 이러한 프로세스를 자동화함으로써 개발자는 생산성을 크게 향상시킨다.
* Less context switching: 코드에 대한 실시간 피드백을 받으면, **개발자가 한 번에 한 가지 작업을 더 쉽게 수행**하고, 인지 부하를 최소화할 수 있다. 자동으로 테스트되는 작은 코드 섹션으로 작업함으로써 개발자는 프로그래밍에 대한 생각이 아직 생생할 때 코드를 빠르게 디버그할 수 있다. 검토할 코드가 적기 때문에 버그 찾기가 더 쉽다.
* Reduce burnout: 연구에 따르면 CD는 배치의 어려움과 팀의 소진을 상당히 줄여준다. 개발자는 CI/CD 프로세스로 작업할 때, **좌절감과 부담을 덜 경험**한다. 이것은 직원을 더 행복하고 건강하게 만들고 번아웃을 줄인다.
* Recover faster: CI/CD를 사용하면, **보다 쉽게 문제를 수정하고 incident에서 복구하여, 평균 해결 시간(MTTR: Mean Time To Resolution)을 단축할 수 있다.** Continuous Deployment 방법은 빈번한 소규모 소프트웨어 업데이트를 의미하므로, 버그가 나타날 때 더 쉽게 찾아낼 수 있다. 개발자는 고객이 빠르게 작업에 복귀할 수 있도록, 버그를 신속하게 수정하거나 변경 사항을 롤백(rolling back)할 수 있다.

## 4. Why GitLab CI/CD?

전체 CI/CD의 모든 필수 기본 사항을 완료하기 위해, 많은 CI 플랫폼은 이러한 요구 사항을 충족하기 위해 다른 도구와의 통합에 의존한다. 많은 조직에서 완전한 CI/CD 기능을 갖추려면, 비용이 많이 들고 복잡한 도구 체인(tool chain)을 유지해야 한다. 이것은 종종 Bitbucket 또는 GitHub과 같은 별도의 SCM을 유지하고, 다양한 보안 및 모니터링 도구에도 연결되는 Chef 또는 Puppet과 같은 배포 도구에 연결되는 CI 도구에 연결되는 별도의 테스트 도구에 연결됨을 의미한다.

훌륭한 소프트웨어를 구축하는 데 집중하는 대신, 조직은 복잡한 도구 체인을 유지하고 관리해야 한다. GitLab은 전체 DevSecOps 라이프사이클(lifecycle)을 위한 단일 애플리케이션이다. 즉, 하나의 환경에서 CI/CD의 모든 기본 사항을 충족한다.

## 5. References

[What is CI/CD?](https://about.gitlab.com/topics/ci-cd/)