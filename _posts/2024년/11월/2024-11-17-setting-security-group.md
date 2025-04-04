---
title: "[AWS] 보안 그룹(Security Group) 설정하기"
excerpt: "보안 그룹을 설정하는 방법은?"
date: 2024-11-17
last_modified_at: 2024-12-12
categories:
  - infra
tags:
  - aws
---

## A. Question

보안 그룹(Security Group)을 설정하는 방법은?

## B. Answer

### 1. "보안 그룹" 검색 + `보안 그룹 (EC2 기능)` 클릭

![aws](https://github.com/user-attachments/assets/3e37eb5b-2ce9-4f8f-8768-0a65569d3885)

### 2. `보안 그룹 생성` 클릭

![aws](https://github.com/user-attachments/assets/027e2572-6bcc-4a60-8241-d3407223b533)

### 3. 세부 정보 입력

* 모든 IP로부터 `HTTP(80)`, `HTTPS(443)` 포트의 트래픽을 허용한다.

![aws](https://github.com/user-attachments/assets/3d1ab5d6-d867-4efc-abc8-7f244228c1df)

> 사진에서는 모든 IP로부터 `SSH(22)` 포트의 트래픽을 허용했지만, 보안상 이는 권장되지 않는다. 무분별한 SSH 접속을 막기 위해, 서비스 관리자 개개인의 IP에 대해서만 22 포트를 허용하는 것이 바람직하다.

* 애플리케이션 서버의 보안 그룹 `staccato-AppServer-PublicSG`에 속한 인스턴스에서만 `MySQL(3306)` 포트로 접근할 수 있도록 설정한다. 이는 애플리케이션 서버가 DB 서버에 접근하여 데이터를 읽고 쓸 수 있도록 허용한다.

![aws](https://github.com/user-attachments/assets/8237fa30-5d9b-4df3-a4c1-11be63e3ff55)

### 4. 완료

![aws](https://github.com/user-attachments/assets/42142598-70d1-4eb9-8586-e2a4d751399f)

![aws](https://github.com/user-attachments/assets/64834602-717f-4850-800e-d3feeaf268d2)

## C. Reference

* [AWS - Security Group](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-security-groups.html)
