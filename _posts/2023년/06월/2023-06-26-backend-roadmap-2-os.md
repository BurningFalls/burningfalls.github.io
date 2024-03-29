---
title: "[Roadmap] Backend Developer Roadmap: 2. OS"
excerpt: "백엔드 개발자 로드맵 분석 - Operating System에 대하여"
date: 2023-6-26
last_modified_at: 2023-6-26
categories:
  - essay
tags:
  - roadmap
  - backend
  - os
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

## 0. Operating System

운영 체제 `OS (Operating System)`는 부팅 프로그램에 의해 컴퓨터에 처음 로드된 후, **컴퓨터의 다른 모든 응용 프로그램을 관리하는 프로그램이다.** 애플리케이션 프로그램은 정의된 `API (Application Program Interface)`를 통해 서비스를 요청함으로써 운영 체제를 사용한다. 또한, 사용자는 `CLI (Command-Line Interface)` 또는 `GUI (Graphical UI)`와 같은 사용자 인터페이스를 통해 운영 체제와 직접 상호 작용할 수 있다.

## 1. Why use an operating system?

운영 체제는 컴퓨터 소프트웨어 및 소프트웨어 개발에 강력한 이점을 제공한다. 운영 체제가 없으면, 모든 응용 프로그램에는 디스크 저장소, 네트워크 인터페이스 등과 같은 기본 컴퓨터의 모든 하위 수준 기능을 처리하는 데 필요한 포괄적인 코드뿐만 아니라 자체 UI가 포함되어야 한다. 사용 가능한 기본 하드웨어의 방대한 배열을 고려할 때, 이것은 모든 애플리케이션의 크기를 엄청나게 부풀리고 소프트웨어 개발을 비실용적으로 만든다.

대신에, 네트워크 패킷을 전송하거나 디스플레이와 같은 표준 출력 장치에 텍스트를 표시하는 것과 같은 많은 일반적인 작업을, 응용 프로그램과 하드웨어 사이의 중개자 역할을 하는 시스템 소프트웨어로 오프로드할 수 있다. **시스템 소프트웨어는 애플리케이션이 하드웨어에 대한 세부 정보를 알 필요 없이, 하드웨어와 상호 작용할 수 있는 일관되고 반복 가능한 방법을 제공한다.**

각 애플리케이션이 동일한 리소스와 서비스에 동일한 방식으로 액세스하는 한, 해당 시스템 소프트웨어(운영 체제)는 거의 모든 애플리케이션에 서비스를 제공할 수 있다. 이를 통해 응용 프로그램을 개발하고 디버깅하는 데 필요한 코딩 시간을 크게 줄이는 동시에, 사용자가 잘 이해된 일반적인 인터페이스를 통해 시스템 하드웨어를 제어, 구성 및 관리할 수 있다.

일단 설치되면, 운영 체제는 방대한 장치 드라이버 라이브러리에 의존하여 OS 서비스를 특정 하드웨어 환경에 맞게 조정한다. 따라서, 모든 애플리케이션은 저장 장치에 대한 공통 호출을 할 수 있지만, OS는 해당 호출을 수신하고 해당 드라이버를 사용하여 해당 호출을 해당 특정 컴퓨터의 기본 하드웨어에 필요한 작업(명령)으로 변환한다. 오늘날 운영 체제는 다양한 하드웨어를 식별, 구성 및 관리하는 포괄적인 플랫폼을 제공한다.

## 2. Functions of an operating system

> [The architecture of an OS] <br>
User <-> Application <-> Operating system <-> Hardware

운영 체제는 다음과 같은 세 가지 필수 기능을 제공한다.

(1) CLI 또는 GUI를 통해 UI를 제공한다.

(2) 응용 프로그램 실행을 시작하고 관리한다.

(3) 일반적으로 표준화된 API를 통해, 해당 애플리케이션에 시스템 하드웨어 리소스를 식별하고 노출한다.

### 2.1. function-1

`UI`: 모든 운영 체제에는 운영체제와 기본 하드웨어를 설정 및 구성하고 문제를 해결하기 위해, **사용자와 관리자가 OS와 상호 작용할 수 있는 UI가 필요하다. CLI와 GUI의 두 가지 기본 UI 유형을 사용할 수 있다.**

`CLI`(terminal mode window): 사용자가 특정 작업과 관련된 특정 명령, 매개 변수 및 인수를 입력하기 위해 기존 키보드에 의존하는 텍스트 기반 인터페이스를 제공한다. 

`GUI`(desktop): 사용자가 터치패드, 터치스크린 및 마우스 장치와 같은 휴먼 인터페이스 장치가 제공하는 제스처에 의존하는 아이콘 및 기호를 기반으로 시각적 인터페이스를 제공한다.

### 2.2 function-2

`Application management`: 운영 체제는 모든 애플리케이션의 시작 및 관리를 처리한다. 이것은 일반적으로 **다양한 작업이 사용 가능한 프로세서의 시간을 공유할 수 있도록, 여러 프로세스 또는 스레드를 시분할하는 것을 포함하여 일련의 동작을 지원한다.** (프로세서의 즉각적인 주의를 끌기 위해 응용 프로그램이 생성하는 인터럽션(interruption)을 처리하여 다른 프로세스를 방해하지 않고 응용 프로그램 및 해당 데이터를 실행할 수 있는 충분한 메모리가 있는지 확인한다. 응용 프로그램의 프로세스를 정상적으로 제거할 수 있는 오류 처리를 수행한다. 다른 애플리케이션이나 OS를 방해하지 않고 메모리 관리를 수행한다.)

운영 체제는 **응용 프로그램이 하위 수준 OS 또는 하드웨어 상태에 대해 알 필요 없이, OS 및 하드웨어 기능을 활용할 수 있도록 하는 API도 지원할 수 있다.** 예를 들어, Windows API는 프로그램이 키보드나 마우스로부터 입력을 받을 수 있도록 하고, 대화 창 및 버튼과 같은 GUI 요소를 생성하고, 파일을 저장 장치에 읽고 쓴다. 응용 프로그램은 거의 항상 응용 프로그램을 실행하려는 운영 체제를 사용하도록 조정된다.

또한, 운영 체제는 응용 프로그램에 대해 다음 서비스를 수행할 수 있다.

* 여러 프로그램이 동시에 실행될 수 있는 멀티태스킹 운영 체제에서, OS는 어떤 응용 프로그램을 어떤 순서로 실행해야 하는지와, 다른 응용 프로그램에 차례를 주기 전에 각 응용 프로그램에 허용되는 시간을 결정한다.
* 하드 디스크, 프린터 및 전화 접속 포트와 같은 연결된 하드웨어 장치와의 입출력(I/O)을 처리한다.
* 작동 상태 및 발생한 오류에 대한 메시지를 각 응용 프로그램 또는 대화형 사용자 또는 시스템 운영자에게 보낸다.
* 인쇄와 같은 일괄 작업 관리를 오프로드하여, 초기 응용 프로그램이 이 작업에서 벗어나도록 할 수 있다.
* 병렬 처리를 제공할 수 있는 컴퓨터에서, 운영 체제는 한 번에 둘 이상의 프로세서에서 실행되도록 프로그램을 분할하는 방법을 관리할 수 있다.

운영체제가 필요한 또는 포함된 모든 주요 컴퓨터 플랫폼(하드웨어 및 소프트웨어)은 다양한 형태 요인의 특정 요구 사항을 충족하기 위해 다양한 기능으로 개발되어야 한다.

### 2.3 function-3

`Device management`: 운영 체제는 기본 컴퓨터 하드웨어 장치에 대한 공통 액세스를 통해, 애플리케이션을 식별하고 구성 및 제공하는 일을 담당한다. OS는 하드웨어를 인식하고 식별하므로, **OS 및 OS에서 실행되는 응용 프로그램이 하드웨어 또는 장치에 대한 특정 지식 없이 장치를 사용할 수 있도록 하는 해당 장치 드라이버를 설치한다.**

운영 체제의 작업은 올바른 프린터를 식별하고 적절한 프린터 드라이버를 설치하여, 응용 프로그램이 해당 프린터에 특정한 코드나 명령을 사용하지 않고 프린터를 호출하기만 하면 된다. 이는 USB 포트, 네트워킹 포트, 그래픽 처리 장치(GPU) 등과 비슷하다.

OS는 서비스를 위한 물리적 및 논리적 장치를 식별하고 구성하며, 일반적으로 Windows 레지스트리와 같은 표준화된 구조에 기록한다. 장치 제조업체는 주기적으로 드라이버를 패치하고 업데이트하며, OS는 최상의 장치 성능과 보안을 보장하기 위해 드라이버를 업데이트해야 한다. 장치가 교체되면, OS도 새 드라이버를 설치하고 구성한다.

## 3. Operating system types and examples

운영 체제의 기본 역할은 어디에나 있지만, 광범위한 하드웨어 및 사용자 요구를 충족하는 수많은 운영 체제가 있다.

운영 체제 유형 간의 차이점은 절대적인 것이 아니며, 일부 운영 체제는 다른 운영 체제의 특성을 공유할 수 있다. 예를 들어, 범용 운영 체제에는 일반적으로 기존 NOS에서 볼 수 있는 네트워킹 기능이 포함되어 있다. 마찬가지로 임베디드 운영 체제는 일반적으로 RTOS의 속성을 포함하는 반면, 모바일 운영 체제는 일반적으로 다른 범용 운영 체제와 마찬가지로 동시에 수많은 앱을 실행할 수 있다.

### 3.1. General-purpose operating system

**범용 OS는 사용자가 하나 이상의 응용 프로그램이나 작업을 동시에 실행할 수 있도록, 다양한 하드웨어에서 다양한 응용 프로그램을 실행하기 위한 일련의 운영 체제를 나타낸다.** 범용 OS는 다양한 데스크탑 및 랩탑 모델에 설치될 수 있으며, 회계 시스템에서 데이터베이스, 웹 브라우저, 게임에 이르기까지 응용 프로그램을 실행할 수 있다. **범용 운영 체제는 일반적으로 프로세스(스레드) 및 하드웨어 관리에 중점을 두어, 응용 프로그램이 존재하는 광범위한 컴퓨팅 하드웨어를 안정적으로 공유할 수 있도록 한다.**

일반적인 데스크탑 운영 체제에는 다음이 포함된다.

* `Windows`는 Microsoft의 flagship 운영 체제로, 가정 및 업무용 컴퓨터의 사실상의 표준이다. 1985년에 소개된 GUI 기반 OS는 그 이후로 많은 버전으로 출시되었다. 사용자 친화적인 Windows 95는 개인용 컴퓨팅의 급속한 발전에 크게 기여했다.
* `Mac OS`는 Apple의 Macintosh 제품군 PC 및 워크스테이션용 운영 체제이다.
* `Unix`는 유연성과 적응성을 위해 설계된 다중 사용자 운영 체제이다. 원래 1970년대에 개발된 Unix는 C 언어로 작성된 최초의 운영 체제 중 하나였다.
* `Linux`는 PC 사용자에게 무료 또는 저렴한 대안을 제공하도록 설계된 Unix와 유사한 운영 체제이다. Linux는 효율적이고 빠른 성능의 시스템으로 명성이 높다.

### 3.2 Mobile operating system

**모바일 운영 체제는 스마트폰 및 태블릿과 같은 모바일 컴퓨팅 및 통신 중심 장치의 고유한 요구사항을 수용하도록 설계되었다.** 모바일 장치는 일반적으로 기존 PC에 비해 제한된 컴퓨팅 리소스를 제공하며, OS는 장치에서 실행되는 하나 이상의 응용 프로그램에 적절한 리소스를 보장하면서 자체 리소스 사용을 최소화하기 위해 크기와 복잡성을 축소해야 한다. **모바일 운영 체제는 효율적인 성능, 사용자 응답성 및 미디어 스트리밍 지원과 같은 데이터 처리 작업에 대한 세심한 주의를 강조하는 경향이 있다.** `Apple iOS` 및 `Google Android`는 모바일 운영 체제의 예시이다.

### 3.3 Embedded operating system

모든 컴퓨팅 장치가 범용인 것은 아니다. 가정용 디지털 보조 장치, 현금 자동 입출금기(ATM), 비행기 시스템, 소매점 POS(Point of Sale) 단말기 및 사물 인터넷(IoT) 장치를 포함한 다양한 전용 장치에는 운영 체제가 필요한 컴퓨터가 포함된다. 주요 차이점은 **연결된 컴퓨팅 장치가 한 가지 주요 작업만 수행하므로, OS가 성능과 복원력 모두에 집중되어 있다**는 것이다. OS는 충돌하지 않고 빠르게 실행되어야 하며, 모든 상황에서 계속 작동하려면 모든 오류를 정상적으로 처리해야 한다. **대부분의 경우 OS는 실제 장치에 내장된 칩에 제공된다.** 예를 들어, 환자의 생명 유지 장비에 사용되는 의료 기기는 환자의 생명을 유지하기 위해 안정적으로 실행되어야 하는 임베디드 OS를 사용한다. `Embedded Linux`는 임베디드 OS의 한 예시이다.

### 3.4 Network operating system

**네트워크 운영 체제(NOS)는 근거리 통신망(LAN)에서 작동하는 장치 간의 통신을 용이하게 하기 위한 또 다른 특수 OS이다.** NOS는 네트워크 패킷을 생성, 교환 및 분해하기 위해 네트워크 프로토콜을 이해하는데 필요한 통신 스택을 제공한다. **오늘날 특수 NOS의 개념은 다른 OS 유형이 대부분 네트워크 통신을 처리하기 때문에 거의 구식이 되었다.** 예를 들어, Windows 10 및 Windows Server 2019에는 포괄적인 네트워크 기능이 포함되어 있다. NOS의 개념은 여전히 라우터, 스위치 및 방화벽과 같은 일부 네트워킹 장치에 사용되며, 제조업체는 `Cisco IOS(Internetwork Operating System)`, `RouterOS` 및 `ZyNOS`를 비롯한 독점 NOS를 사용할 수 있다.

### 3.5 Real-time operating system

**컴퓨팅 장치가 일정하고 반복 가능한 시간 제약 내에서 실제 세계와 상호 작용해야 하는 경우, 장치 제조업체는 실시간 운영 체제(RTOS)를 사용하도록 선택할 수 있다.** 예를 들어, 산업 제어 시스템은 거대한 공장이나 발전소의 운영을 지시할 수 있다. 이러한 시설은 무수한 센서에서 신호를 생성하고 valve, actuator, motor 및 기타 수많은 장치를 작동하기 위해 신호를 보낸다. 5이러한 상황에서 산업 제어 시스템은 변화하는 실제 조건에 신속하고 예측 가능하게 대응해야 한다. 그렇지 않으면 재난이 발생할 수 있다. **RTOS는 다른 유형의 운영 체제에서 완벽하게 허용되는 버퍼링, 처리 대기 시간 및 기타 지연 없이 작동해야 한다.** RTOS의 두 가지 예로는 `FreeRTOS`와 `VxWorks`가 있다.

## 4. References

[Computer Basics: Understanding Operating Systems](https://www.techtarget.com/whatis/definition/operating-system-OS)

