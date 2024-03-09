---
layout: single
title: "데이터 마이닝 - KDD Process"
categories: Data-Mining
tag: datamining,KDD-Process
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# ※ KDD Process
Knowledge Discovery in Database

## **1. Problem Formulation**

### 1. Specific objectives 
    - 문제 확인, 자세하게 정의
    - 문제들간의 관계 이해
    - 모호한 부분 해소
    - 고객과 상담자의 정의가 다른지 확인, 문제의 정의에 대한 모호한 부분 제거
    - 문제점 나열, 중요도 점검
    - 해결할 문제 선택
    - project의 범위 결정

### ■ The right problem to mine
    - 분석의 대상은 업무적 가치가 있는 것
    - action을 취할 수 있는 것
    - action의 결과가 포착될 수 있는 것
    - 원하는 정보가 찾아질 수 있는 것
    - 데이터가 존재해야함
    - 왜 마이닝을 하는지 관련자들이 공감하는 내용이어야 함
  
###  ∴ 초기 주제 선택 기준
    - 중요성
    - 짧은 소요기간 (복잡성과 연관)
    - 결과의 가시성

### 2. Translation into analytical methods (problem translation)
    1. Predctive Modeling (예측 모형)
        - Supervised classification (y: 범주형)
          + event / no event (binary target)
          + class label (multiclass problem)
        - Product Prediction
        ↔ Regression (or Supervised Continuous-value Prediction) (y: 연속형)
            - continuous outcome
        ↔ Time series analysis
        ↔ Survival analysis (생존분석)
            - time-to-event
    2. Association Rules (연관규칙)
    3. Cluster Analysis (군집분석)
        - Unsupervised Classification (y가 없음)
            * 잘됐는지 못됐는지 확인이 불가능

### 3. Data Examination
    1. preliminary acquision of the data
        - 요구되는 데이터 나열
        - 데이터의 위치와 수집방법
        - 자료습득의 문제와 해결방법
    2. data description
        - 데이터 기술 레포트
        - 데이터의 양, 각 속성에 대한 의미 확인
    3. data explore
        - min, max 등 정보 확인
    4. verification of data quality
        - 각 속성값들의 일관성 점검
        - 데이터의 완성도와 올바른지 점검

### 4. refinement and reformulation

### 5. 해결수단 선택
    1. 문제 해결 방식과 결과물 결정
    2. 결과물의 형태: 리포트, 프로그램, 수식 교육
    3. 구체적이고 자세하게

### 6. 실행방법 수립
    1. 적절한 계획수립 필요
    2. 주어진 자원(돈, 시간, 사람) 잘 분배
    3. 육하원칙에 의하여 구체적으로 제시


### ■ 요구되는 전문 지식 (required expertise)
    - Domain: 현업에서의 전문가
    - Data: DB, Warehousing 전문가
    - Analytical Methods: 모델링 및 분석전문가

### ■ 배경지식의 필요성 (Background Knowledge Discovery)
    - 이해없이 특정한 주제에 바르게 접근이 어려움
    - 외부환경 변화에 대한 데이터 필요
        ↔ 내부변동은 외부 변동에 영항을 받음
        → 환경에 대한 분석 필요
    
### ■ 프로젝트 성공요건
    - 필요한 모든 data의 사용 가능성
    - 대량의 data를 처리할 수 있는 환경(서버)
    - 대양한 기술(technology)
    - ★ but problem focus(기술보단 해결에 초점을 두어야 한다)
    - 사람과 기술의 문제해결을 위한 과정의 성공적인 통합

<br>

## **2. Data Preparation**
* Preparation이 중요한 이유: **Garbage In, Garbage Out**
* 데이터 질의 다차원 측도
    - accuracy, completeness, consistency, timeliness, believability, value added, interpretability, accessibility

### **1. extracting and sampling data from DB or DW**
    1. check sources of data
        - operational system
        - data warehouse and data mart
        - OLAP applications
        - Survey: 비쌈, n이 작음, 목적과 바로 연결되는 데이터
        - household and demographic databases

### ■ Data is dirty!
    * incomplete: acking attribute values, lacking certain attributes of interest, or containing only aggregate data
    - 원인: "not applicable" (해당사당 없음)
            데이터 수집한 때와 분석한 때의 시간차이
            사람, 하드웨어, 소프트웨어 문제
    
    * inconsistent: 코드나 이름에서의 차이 포함
    - 원인: 데이터 출처가 다름
            종속성 위반(functional dependency violation)

    * noisy: error, outlier 포함
    - 원인: 데이터 수집기의 결함
            데이터 입력시 잘못 입력
            데이터 전송시 에러
            기술적인 한계
    - 해결: 컴퓨터와 사람 검사의 조합
            군집화 (clustering)
            Smoothing (추정치 사용)

### **2. Checking the integrity**
    1. 범주형 변수일 때 (빈도수 확인)
        - check the presence of all categories
        - check the proportion of all categories: low proportion check
    2. 연속형 변수일 때 (기술통계량 확인)
        - check descriptive statistics
            : min, max, mean, median, sd, ...
        - detect outliers
            : 히스토그램, 상자그림, ...
    3. 유효하지 않은 성질과 값 확인
    4. 수치형 필드에 missing이나 비수치형 데이터 확인
    5. fixed values 확인
    6. 유효하지 않은 날짜 확인
    7. 같은 레코드, ID 확인

### ■ Duplicate data
    중복된 데이터.
    여러 다른 종류의 출처로부터 합칠 때 문제가 된다.

### **3. Integrating data**
    1. data integration
        : 여러 출처로부터, 일관성있는 하나의 데이터를 합치는 것
    2. schema integration
        : 메타데이터 통합
            메타데이터(metadata): 데이터를 설명해주는 데이터
    3. detecting and resolving data value conflics
        : 같은 것 처럼 보이지만 다른 변수 확인
            why? 다른 단위, different represntations

### ■ Missing data
    * 원인
        장비 문제
        일관성이 없어서 삭제됨
        이해를 못해서 입력되지 않음
        입력할 때는 중요하지 않다고 생각되어 입력하지 않음
        수집되지 않음
        "Not Applicable" 해당사항 없음
    * 해결
        review raw data: 원자료 수정
        impute data: 대체자료 사용
            (K-nearest neighbor, decision tree 등)
        레코드 삭제
        변수 삭제
        Assign a category for missing value for categorical variables

### ■ Data Cleansing
    일관성 없는 데이터를 바르게 수정함
    → 통합으로 생긴 중복된 데이터 해결
    → 같은 값 삭제
    → missing value imputation
    → 일관성 없는 것 제거
    → 오래된 데이터 갱신
    → unique한 레코드 생성

### ■ Redundant / State data
    시간이 지나면서 변수는 변했지만 DB에 반영되지 않음
    적잘하지 않은 변수는 속도를 느리게 함(차원 감소 필요)
    한 DB에서의 변수는 다른 곳에서 온 변수임

    ★ 변수가, 다른 DB에서 다른 이름을 가짐
        해결: 데이터 통합시 발생하는 문제에 대해
            상관분석을 통해 찾을 수 있음
            상관계수가 높으면 두 변수 중 하나만 사용한다

### **4. Transforming and Creating**

### **5. Removing independent variables**

## **3. Data mining**

## **4. Information**

<br>
<br>
<br>
<br>

-- end of KDD Process --