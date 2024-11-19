---
title: "[AWS] 탄력적 IP는 특정 EC2 인스턴스에 연결되어 활성화된 상태라면 무료다??? - WRONG"
excerpt: "탄력적 IP는 특정 EC2 인스턴스에 연결되어 활성화된 상태라면 무료인가? 탄력적 IP의 바뀐 요금 부과 정책은? EC2 인스턴스에 탄력적 IP를 사용하는 것이 이득인가?"
date: 2024-11-19
last_modified_at: 2024-11-19
categories:
  - infra
tags:
  - aws
---

## A. Question

> 탄력적 IP는 특정 EC2 인스턴스에 연결되어 활성화된 상태라면 무료이다. 탄력적 IP 주소가 할당된 상태지만 EC2 인스턴스에 연결되지 않은 경우, 해당 IP 주소에 대해 시간당 요금이 청구된다.

인터넷을 검색해보면 다음과 같은 문장을 볼 수 있다. **결론적으로 이 설명은 현재 시점(2024/11/19)을 기준으로는 틀렸다.**

이에 대해서 직접 조사해본 내용을 공유하고자 한다.

## B. Answer

[공지 – AWS Public IPv4 주소 요금 변경 및 Public IP Insights 기능 출시](https://aws.amazon.com/ko/blogs/korea/new-aws-public-ipv4-address-charge-public-ip-insights/)는 2023년 8월 1일에 작성된 글이다. 글 내용에서 `2024년 2월 1일부터 서비스 연결 여부에 관계없이 모든 퍼블릭 IPv4 주소에 대해 시간당 IP당 0.005 USD의 요금이 부과된다`는 것을 알려주고 있다. 퍼블릭 IPv4 요금 변경 세부 사항으로 나와있는 표를 보면 더 자세하게 알 수 있다.

| 퍼블릭 IP 주소 유형 | 현재 요금/시간(USD) | 신규 요금/시간(USD) (2024년 2월 1일부터 시행) |
|----------------------|---------------------|-----------------------------------------|
| VPC, Amazon Global Accelerator 및 AWS Site-to-Site VPN 터널의 리소스에 할당된 사용 중인 퍼블릭 IPv4 주소(Amazon 제공 퍼블릭 IPv4 및 탄력적 IP 포함) | 무료 | 0.005 USD |
| 실행 중인 EC2 인스턴스의 추가(보조) 탄력적 IP 주소 | 0.005 USD | 0.005 USD |
| 계정의 유휴 탄력적 IP 주소 | 0.005 USD | 0.005 USD |

2024년 2월 이전에는 탄력적 IP를 포함한 모든 퍼블릭 IP에 대한 요금이 전부 무료였다. 하지만, 계정의 유휴(EC2에 연결되어 있지 않은) 탄력적 IP에 대해서는 0.005 USD의 요금을 부과했다. 따라서, `탄력적 IP는 특정 EC2 인스턴스에 연결되어 활성화된 상태라면 무료이다. 탄력적 IP 주소가 할당된 상태지만 EC2 인스턴스에 연결되지 않은 경우, 해당 IP 주소에 대해 시간당 요금이 청구된다`는 설명은 예전 기준으로 정확하다. 실제로 이 문장이 써있는 많은 블로그의 글들은 대부분 2023년 8월 이전에 써져서 이 소식이 공표되기 전에 작성했기 때문에, 내용을 주기적으로 갱신하지 않는다면 현재 시점에서 잘못된 정보가 된건 어쩔 수 없다.

AWS 공식문서의 설명상으로, 2024년 2월 1일 이후에는 일반 Public IP, 탄력적 IP, 유휴 탄력적 IP를 포함한 모든 Public IP에 대해서 시간당 0.005 USD의 요금이 부과되는 것이 맞다. [탄력적 IP 주소에 대해서 설명하는 AWS 문서](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#eip-pricing)에서도 다음 문장을 찾을 수 있다. `AWS는 실행 중인 인스턴스와 관련된 퍼블릭 IPv4 주소 및 Elastic IP 주소를 포함하여 모든 퍼블릭 IPv4 주소에 대해 요금을 청구합니다.` [Amazon VPC 요금](https://aws.amazon.com/ko/vpc/pricing/)의 `퍼블릭 IPv4 주소` 탭에서 IPv4 주소의 계산 방식을 찾을 수 있다.

## C. Detail - EC2 인스턴스에 탄력적 IP를 사용하는 것이 이득인가

이렇게 되면 일반 Public IP와 탄력적 IP 모두 동일한 요금이 부과되기 때문에, EC2 인스턴스에 탄력적 IP를 무조건 할당하는 것이 이득이 아닌가 하는 생각이 든다. 이에 대해서 분석해보고자 한다.

### 1. 탄력적 IP의 특징

* 고정된 IP 유지: 탄력적 IP는 인스턴스가 중지되거나 종료되더라도 IP Address가 유지된다. 이는 서비스의 안정성을 확보하는 데 큰 도움이 된다.
* 다른 인스턴스로 재할당 가능: 문제가 발생하여 인스턴스를 교체해야 할 경우, 동일한 탄력적 IP를 새로운 인스턴스에 재할당할 수 있어, 클라이언트가 기존 IP를 그대로 사용할 수 있다.
* 유휴 IP 요금: EC2 인스턴스에 연결되지 않은 유휴 상태의 탄력적 IP는 시간당 0.005 USD의 요금이 부과된다. 따라서 사용하지 않는 IP는 즉시 해제하는 것이 바람직하다.

### 2. 탄력적 IP의 단점

* IP Address 관리의 복잡성 증가: 탄력적 IP는 고정된 IP를 유지해야 하는 서비스에는 필수적일 수 있지만, 여러 인스턴스에 대해 관리할 경우 IP Address를 추적하고 적절히 할당하는 작업이 복잡할 수 있다. 관리 오류로 인해 유휴 상태의 탄력적 IP가 남아 있으면 비용이 발생할 위험이 있다.

### 3. 결론

탄력적 IP의 특징과 단점을 종합해 보면, 관리만 철저히 이루어진다면 탄력적 IP를 할당해도 비용 측면에서 일반 Public IP와 큰 차이가 없다. 특히, 고정 IP가 필요한 환경이나 장애 복구 및 인스턴스 교체 시 동일한 IP를 유지해야 하는 서비스에는 탄력적 IP가 큰 이점을 제공한다. 탄력적 IP가 유휴 상태면 비용이 발생할 수 있지만, IP Address를 적절히 추적하고 관리하여 유휴 상태를 방지하면 이러한 문제를 최소화할 수 있다. 결론적으로, EC2 인스턴스에 탄력적 IP를 할당하는 것은 고정된 IP Address가 필요한 서비스 환경에서는 매우 유리할 수 있으며, 관리만 잘 이루어진다면 비용적으로 문제가 되지 않는다.

## D. Reference

* [AWS - 탄력적 IP 주소](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#eip-pricing)
* [AWS - Amazon VPC 요금](https://aws.amazon.com/ko/vpc/pricing/)
* [공지 – AWS Public IPv4 주소 요금 변경 및 Public IP Insights 기능 출시](https://aws.amazon.com/ko/blogs/korea/new-aws-public-ipv4-address-charge-public-ip-insights/)
