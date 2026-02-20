# 🏥 삼성서울병원 AEGIS 데이터플랫폼 & 데이터뱅크 구축 프로젝트 정리
(Infra SA + Data Governance + Multi-Account Architecture 관점)



## 1. 프로젝트 개요 (Why this project mattered)


### 프로젝트명
삼성서울병원 AEGIS 데이터플랫폼 & 데이터뱅크 구축


### 핵심 목적
- 의료기관 데이터 → 안전하게 수집
- 외부 분석기관 → 통제된 방식으로 접근
- 계좌 기반 데이터 거래 구조 구현
- 연구자/데이터 소비자 간 분리된 보안 환경 제공


## 2. 전체 구조 개요 (3 Account Model)


    [Bank Account]        ← 데이터 제공기관
       - S3 (Raw Data)
       - Glue Catalog
       - Lake Formation
          │
          │ (Cross Account Share)
          ▼
    [Platform Account]    ← 플랫폼 통제 계정
       - SageMaker Studio Domain
       - DataZone
       - Project Profile / Blueprint
          │
          │ (Project 기반 접근)
          ▼
    [User Account]        ← 데이터 소비기관
       - SageMaker Studio
       - Athena
       - 분석 환경



## 3. 아키텍처 핵심 기술 요소


### 1. Lake Formation 기반 데이터 거버넌스


### 2. Cross-Account Data Access 설계


### 3. SageMaker Studio Domain (Platform 중심 설계)

