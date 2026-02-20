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

#### 역할 
- 테이블 단위 권한 제어
- 컬럼 단위 접근 제어
- Cross-account 데이터 공유

#### 중요 포인트
Glue Catalog를 단순 공유하는 게 아니라, Lake Formation 권한 모델을 통해 통제


### 2. Cross-Account Data Access 설계

#### 핵심 문제
- Bank Account에 있는 데이터
- User Account에서 분석해야 함
- 하지만 직접 S3 접근은 불가

#### 해결 방법
- LF Grant
- Resource Share
- IAM Role Assume
- Studio Project 기반 권한 위임


### 3. SageMaker Studio Domain (Platform 중심 설계)

#### Platform Account에서:
- Studio Domain 생성
- Project Profile 생성
- Blueprint 정의
- VPC/Subnet 설정
- Execution Role 관리

#### 중요 Role 
- AmazonSageMakerProvisioning-<AccountId>
- AmazonSageMakerManageAccess-<Region>-<DomainId>
ㄴ 두 Role의 역할
  - 프로젝트 생성
  - Glue DB 생성
  - LF 권한 위임
  - 사용자 접근 제어
 



