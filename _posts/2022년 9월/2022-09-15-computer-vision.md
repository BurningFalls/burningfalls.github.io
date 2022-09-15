---
title: "[Lecture] Computer Vision"
excerpt: "신종수 강사님의 Computer Vision 강의 내용 정리"
date: 2022-09-15
last_modified_at: 2022-09-15
categories:
  - essay
tags:
  - lecture
---

## Computer Vision in Kakao Enterprise (lecturer: Jongju Shin)

### KAKAO ENTERPRISE

MANIFESTO: CONNECT + SOLVE + CREATE + AI

digital transformation

실용적인 AI 기술을 바탕으로 일상에서 체감할 수 있는 변화를 만들어감

현재 300개+ 회사와 협업을 통해 다양한 AI 기반 서비스를 제공하고 있음

KAKAO I: 카카오엔터프라이즈가 보유한 AI기술의 집합체

### AI Lab & Service

서비스의 핵심이 되는 AI 기술 연구와 자체 서비스 개발을 담당함

1. Core AI: Vision AI, Conversational AI, Voice Interface

2. Applied AI: Commerce AI, Business Automation, Forecasting & Optimization

3. AI Platform & Service: MLOps, AI-as-a-Service

꾸준한 R&D 투자로 현재 글로벌 최고 성능을 의미하는 SOTA 기술을 다수 보유함

### 얼굴인식

detection -> alignment -> normalizatoin -> recognition

1. Verification(검증): 주어진 두 얼굴이 같은지를 판단

2. Identification(인증): 입력 얼굴과 등록된 얼굴들을 비교해서 누구인지를 인식

Service - 다음 라이브픽 서비스: 다음(Daum) 이미지 검색으로 유입된 대량 데이터를 분석하여, 이벤트별 이미지 묶음을 시간 순으로 제공하는 서비스

[개발 과정]

1. 유명인 얼굴 인식 데이터 수집 (데이터 수정)

2. 딥러닝을 이용해 얼굴 인식 모델을 학습 (모델 학습)

3. 사용자가 입력한 이미지에 대해서 제대로 인식하는지 평가 (성능 평가)

4. 다시 1로 돌아감

Service - 뉴스 클러스터링: 동시에 올라오는 다량의 뉴스에 대해서 클러스터링하여 하나의 주제로 묶어줌

### 워크스루

얼굴 인식 기술로 마스크를 쓴 상태에서도 사내에서 출입 통제 시스템으로 사용함

사원증 태그 없이, 양손은 편안하게, 지정된 영역에 얼굴을 맞출 필요없이, 지나가기만 하면 얼굴인증 출입

[개발의 어려움]

서버에서 동작하던 알고리즘을 모바일에서 동작하게 해야 함.

 - 성능 vs 속도의 tradeoff

먼저 ios 플랫폼에서 시도 (애플의 NPU를 사용하는 coreml)

 - 애플은 swift 사용

학습한 얼굴에는 마스크가 없어서 학습데이터에 마스크를 합성해야 함.

다른 사람의 사진(사원증)으로 인식 시도(anti-spoofing)를 막아야 함

### FRVT (Face Recognition Vendor Test)

미국 NIST에서 주최하는 얼굴 인식 프로그램(verification)의 성능 평가

4개월에 한 번씩 프로그램을 제출할 수 있음

우리가 만든 알고리즘이 세계에서 어느 정도에 위치할까?

Visa, mugshot(범죄자 얼굴 인식), border(입국심사), wild, kiosk

2019년 7월에 처음 참여해서 (100/109)등 -> 문제가 있는 부분을 찾고 개선

2020년 3월 wild 부문 3등 -> 성능 개선을 위해서 다양한 시도

2022년 5월 kiosk 1등

축적의 시간이 필요함. 첫 시도에서 좋지 않다고 포기하지 마라.