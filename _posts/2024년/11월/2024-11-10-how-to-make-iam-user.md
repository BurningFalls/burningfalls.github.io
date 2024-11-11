---
title: "[AWS] IAM 사용자 생성하기"
excerpt: "IAM 사용자 생성하기"
date: 2024-11-10
last_modified_at: 2024-11-10
categories:
  - infra
tags:
  - aws
---

## A. Question

IAM 사용자 생성은 어떻게 할까?

## B. Answer

### 1. 루트 사용자로 접속한다.

![aws](https://github.com/user-attachments/assets/511047de-4d3e-43dc-a8f4-caac16594210)

### 2. IAM을 검색해서 들어간다.

![aws](https://github.com/user-attachments/assets/50dabbe0-5c76-4bb0-a84d-786b973ebeaf)

### 3. `사용자` > `사용자 생성` 클릭

![aws](https://github.com/user-attachments/assets/76ffe738-79d2-4620-88d1-8aaf7413eb8a)

### 4. 사용자 세부 정보를 지정한다.

* 사용자 이름에 `Administrator`를 입력한다.
* AWS Management Console 액세스 옆의 확인란을 선택한다. 그런 다음 자동 생성된 암호를 체크한다.
* 사용자는 다음 로그인 시 새 암호를 생성해야 하기 때문에, 사용자 지정 암호를 생성해줄 필요가 없다.

![screencapture-us-east-1-console-aws-amazon-iam-home-2024-11-10-20_47_06](https://github.com/user-attachments/assets/2c93a22c-7a19-42b5-9bea-30c9e459f599)

### 5. 권한 설정에서 `그룹에 사용자 추가`를 체크하고 `그룹 생성`을 클릭한다.

![aws](https://github.com/user-attachments/assets/abca7a6a-2b83-4429-8041-6d21fd46baa7)

### 6. 그룹 이름에 `Administrators`를 입력하고, 권한 정책으로 `AdministratorAccess`를 선택한다. `사용자 그룹 생성`을 클릭한다.

![aws](https://github.com/user-attachments/assets/97545bd9-4a4f-4d9c-8829-bb7c24f8b9b7)

### 7. 그룹을 체크하고 `다음`을 클릭한다. `사용자 생성`을 클릭한다.

![aws](https://github.com/user-attachments/assets/71b564e2-e76d-4bba-ab76-f8691d6e6c34)

![aws](https://github.com/user-attachments/assets/07bc9686-ae94-439b-a9a4-9ab20c627e74)

### 8. 완료

![aws](https://github.com/user-attachments/assets/5ef083a6-8ee5-4aee-b316-e1bd7cb38e4a)

### 9. URL 접속 > IAM 사용자 이름 & 암호 입력

![aws](https://github.com/user-attachments/assets/5a52f7cc-554a-4698-9316-fc1e65bc0cf0)

### 10. 새로운 비밀번호 입력해서 변경

![aws](https://github.com/user-attachments/assets/97cb304f-2200-486a-acee-3cfc5d398bad)

## C. Detail - 계정 별칭 변경

* 로그인할 때 편리하게 입력하기 위해서 계정 별칭을 변경한다.

### 1. `IAM` 입력해서 클릭

![aws](https://github.com/user-attachments/assets/5dbaf1b3-a931-4bc7-9c05-ff9173179671)

### 2. `AWS 계정` > `계정 별칭` > `생성` 클릭

![aws](https://github.com/user-attachments/assets/1f6a88f4-f1bb-43e0-8615-15dcc81ca037)

### 3. 계정 별칭을 입력하고 `별칭 생성` 클릭

![aws](https://github.com/user-attachments/assets/c4e4f5ad-6c7b-4dbb-ac15-18bf83412e23)

### 4. 완료

![aws](https://github.com/user-attachments/assets/590d4d89-1ed8-4e22-a192-2909a7f68b8f)

## D. MFA 추가

* [MFA 설정하기](https://burningfalls.github.io/infra/how-to-make-freetier-aws-account/#d-detail---mfa-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0) 글을 참고한다.

![aws](https://github.com/user-attachments/assets/f0646f35-1200-40a1-85ad-1425d008b615)

## E. 결제 정보 액세스 허용

AWS 계정의 IAM 사용자와 역할은 기본적으로 `Billing and Cost Management` 콘솔에 엑세스할 수 없다. 이는 특정 `Billing` 기능에 대한 액세스를 허용하는 IAM 정책이 있는 경우에도 마찬가지이다. 액세스를 허용하려면 AWS 계정 루트 사용자가 먼저 IAM 액세스를 활성화해야 한다.

### 1. 루트 권한 사용자로 로그인

![aws](https://github.com/user-attachments/assets/974c9936-1c5b-4393-a887-9139c2bbfb66)

### 2. 오른쪽의 `계정` 클릭

![aws](https://github.com/user-attachments/assets/54ec68b6-454a-40df-84a6-610cf2092da3)

### 3. 스크롤을 아래로 내려서 `결제 정보에 대한 IAM 사용자 및 역할 액세스` 찾기

![aws](https://github.com/user-attachments/assets/cdfbb552-4364-4785-9b55-19465427459f)

### 4. `편집` > `IAM 액세스 활성화` > `업데이트` 클릭

![aws](https://github.com/user-attachments/assets/5863cfe0-bcb0-408b-9dbf-81d84afbd4b6)

### 5. 완료

![aws](https://github.com/user-attachments/assets/3f70d6f5-4d84-4742-ab24-921f635768d2)

## F. Reference

* [AWS - IAM 사용자 생성](https://docs.aws.amazon.com/ko_kr/filegateway/latest/filefsxw/setting-up-create-iam-user.html)

* [AWS - AWS 계정 설정](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started-account-iam.html#billing-access)