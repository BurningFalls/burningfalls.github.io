---
title: "[AWS] AWS 프리티어 계정 만들기"
excerpt: "AWS 프리티어 계정 만들기"
date: 2024-11-09
last_modified_at: 2024-11-09
categories:
  - infra
tags:
  - aws
---

## A. Question

AWS 프리티어 계정은 어떻게 만들까?

> **AWS 프리티어 계정**은 다양한 서비스를 무료로 제공하지만, 리소스에는 제한이 있다. 각 서비스마다 사용 가능한 한도와 기간(일반적으로 12개월)이 있으므로, 이를 명확히 이해하고 활용하는 것이 중요하다. 아래 사이트에서 자세한 내용을 확인할 수 있다.<br> [AWS 프리티어 시작하기](https://docs.aws.amazon.com/ko_kr/whitepapers/latest/how-aws-pricing-works/get-started-with-the-aws-free-tier.html){: target="_blank"}

## B. Answer

### 1. AWS 홈페이지에 접속한다.

   * [AWS 홈페이지](https://aws.amazon.com/ko/){: target="_blank"}

### 2. `프리 티어` 클릭

![aws](https://github.com/user-attachments/assets/0ff64473-1422-487c-8ab5-878ea659af73)

### 3. `무료 계정 생성` 클릭

![aws](https://github.com/user-attachments/assets/d738cada-7965-4c71-b464-dea4b1ede76b)

### 4. **루트 사용자 이메일 주소**와 **AWS 계정 이름**을 입력한다.

    * 오른쪽 상단에서 언어 변경이 가능하다.
    * **AWS 계정 이름**은 영어로 입력해야 한다.

![aws](https://github.com/user-attachments/assets/bd5fd431-3c23-4192-a473-20d1b99f9549)

### 5. 입력한 이메일 주소로 도착한 확인 코드를 확인하여 입력한다.

![aws](https://github.com/user-attachments/assets/1cc3ff6d-e929-4837-9d3a-6007845596be)

### 6. **루트 사용자 암호**를 입력한다.

   * 암호 규칙은 아래 사진에 나와 있는 것과 같다.

![aws](https://github.com/user-attachments/assets/d1095c29-788c-43d8-ba2b-89f032aa6f29)

### 7. 세부 정보를 입력한다.

   * 주소는 [영문주소변환 사이트](https://www.jusoen.com/){: target="_blank"}를 사용해서 입력하면 편리하다.

![screencapture-portal-aws-amazon-billing-signup-2024-11-09-15_32_00](https://github.com/user-attachments/assets/bddccee9-4905-4339-b05b-579c144d2d64)

### 8. 결제 정보를 입력한다.

![screencapture-portal-aws-amazon-billing-signup-2024-11-09-15_41_06](https://github.com/user-attachments/assets/8acccdfb-5170-4d5d-a64a-fee4d431c738)

   * 카드 인증을 위해 정보를 입력한다.

![screencapture-aps-kcp-co-kr-v1-card-cert-mfa-BQty1fhadnWV1YsIhCId-2024-11-09-15_43_53](https://github.com/user-attachments/assets/e18e6443-596c-4c25-b147-f48041a923d9)

### 9. 자격 증명을 확인한다.

![screencapture-portal-aws-amazon-billing-signup-2024-11-09-15_45_04](https://github.com/user-attachments/assets/bac4f07e-6e76-4a13-8e4c-1814222a80f8)

![screencapture-portal-aws-amazon-billing-signup-2024-11-09-15_46_38](https://github.com/user-attachments/assets/3d852d5c-26f3-47a3-81a9-753431dfe028)

### 10. Support 플랜을 선택한다.

![screencapture-portal-aws-amazon-billing-signup-2024-11-09-15_47_30](https://github.com/user-attachments/assets/c303e6bb-89aa-4b6d-ba17-95fe32ee04bf)

### 11. 완료

![screencapture-aws-amazon-ko-registration-confirmation-2024-11-09-15_49_01](https://github.com/user-attachments/assets/797445f2-5ac4-4527-88ad-242ad32251ff)

   * `AWS Management Console로 이동`을 클릭해서 시작할 수 있다.

![screencapture-ap-northeast-2-console-aws-amazon-console-home-2024-11-09-15_53_00](https://github.com/user-attachments/assets/ba61fa0d-5824-4fc6-8ec8-d232779f4a88)

## C. Detail - AWS 프리티어 비용 알림 설정

* AWS 계정에 가입하면 계정(AWS 계정 루트 사용자)을 생성할 때 사용한 이메일 주소로 프리 티어 알림이 전송된다. 이러한 알림은 AWS 서비스 사용량이 AWS 프리 티어 사용량 한도에 근접하거나 한도를 초과할 때 전송된다.

### 1. 오른쪽 상단의 `본인 계정 이름` > `계정` 클릭

![aws](https://github.com/user-attachments/assets/b146044c-a6e9-4281-84c2-01c44df8b4d7)

### 2. 왼쪽 메뉴에서 `빌링 기본 설정` 클릭

![aws](https://github.com/user-attachments/assets/159675e7-adb0-4eb5-85ca-112f9c90abff)

### 3. AWS 프리 티어 알림을 수신할 이메일을 입력한다.

![aws](https://github.com/user-attachments/assets/d393b6e1-c424-45c3-b6c2-59bb1425d597)

### 4. 완료

![aws](https://github.com/user-attachments/assets/3937f447-0230-4def-ae69-3850534567a4)

## D. Reference

* [AWS](https://aws.amazon.com/ko/)