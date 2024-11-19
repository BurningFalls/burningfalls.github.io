---
title: "[AWS] VPC 편리하게 설정하기"
excerpt: "AWS VPC를 편리하게 설정하는 방법은?"
date: 2024-11-17
last_modified_at: 2024-11-17
categories:
  - infra
tags:
  - aws
---

## A. Question

AWS VPC를 편리하게 설정하는 방법은?

> NAT Gateway를 생성하는 경우, 활성화되어 있는 동안(사용하지 않더라도) 서울 기준 시간당 0.059USD의 비용이 발생하기 때문에, 신중하게 사용해야 한다. 아웃바운드 트래픽이 발생하는 경우, 시간당 사용 요금 외에 데이터 처리 요금도 추가로 지불해야 한다.

## B. Answer

* 만들고자 하는 InFra Structure

![aws](https://github.com/user-attachments/assets/f694c58c-532f-40f1-a5bd-8cd4afc5b2f6)

### 1. VPC 검색

![aws](https://github.com/user-attachments/assets/89bac562-42cf-48e4-8970-f0030b7d702f)

### 2. `VPC` 클릭

![aws](https://github.com/user-attachments/assets/13c7cad5-ac6c-41ad-83f4-41809b3c01f3)

### 3. `VPC 생성` 클릭

![aws](https://github.com/user-attachments/assets/80a88dea-05a2-495a-bf67-220b35882bbb)

### 4. `VPC 등` 클릭

![aws](https://github.com/user-attachments/assets/7676aa0b-bb69-4692-a64d-3f4512a5b8b9)

### 5. 정보 입력

* VPC CIDR: `10.0.0.0/16`

![aws](https://github.com/user-attachments/assets/08642b81-d141-439d-a5f7-4c0ddc5e8c47)

* Public Subnet CIDR: `10.0.0.0/20`

![aws](https://github.com/user-attachments/assets/49dc4762-166f-4340-a800-766599b4d089)

* Private Subnet CIDR: `10.0.128.0/20`

![aws](https://github.com/user-attachments/assets/15ea803e-6496-40b1-b23a-5b7c769d7327)

* 정보 입력

![aws](https://github.com/user-attachments/assets/15d6e0c3-e0e4-4c47-85eb-7bb0383e51e1)

![aws](https://github.com/user-attachments/assets/d59dd124-2780-4430-b655-e0ea958bc79a)

![aws](https://github.com/user-attachments/assets/d9a31f0b-19f0-4362-8f44-54068aef2630)

### 6. 완료

![aws](https://github.com/user-attachments/assets/1cdd41a5-e6aa-482c-9341-273293ef82e1)

## C. Reference

None
