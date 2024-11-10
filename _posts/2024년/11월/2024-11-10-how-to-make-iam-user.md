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

## 1. Question

IAM 사용자 생성은 어떻게 할까?

## 2. Answer

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

### 10. 새로운 AWS 계정 이름 & 비밀번호 입력해서 변경

![aws](https://github.com/user-attachments/assets/97cb304f-2200-486a-acee-3cfc5d398bad)

### 11. IAM 계정에도 MFA를 추가해준다.

![aws](https://github.com/user-attachments/assets/f0646f35-1200-40a1-85ad-1425d008b615)

## 3. Detail

None

## 4. Reference

* [AWS - IAM 사용자 생성](https://docs.aws.amazon.com/ko_kr/filegateway/latest/filefsxw/setting-up-create-iam-user.html)