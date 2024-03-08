---
layout: single
title: "데이터 마이닝 - Introduction"
categories: DataMining
tag: datamining
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br><br>

# ※ Data Mining Background

## `Why data mining?`

### - Traditional data collection methods
- Survery sampling (표본추출)
- Experiment (실험)
- Observational Study (관찰연구)

### - The explosive growth of data
- data collection and data availabilty
  +  Automated data collection tools
  + Database System
  + Web
  + Computerized Society
  
<br>

## `The Data`

| -           | Experimental        | Opportunistic      |
|:-----------:|:-------------------:|:------------------:|
| Purpose     | research            | operational        |
| Value       | scientific          | commercial         |
| Gerneration | actively controlled | passively observed |
| Size        | small               | massive            |
| Hygiene     | clean               | dirty              |
| State       | static              | dynamic            |


<br>

## `Defining characteristics of data in data mining`
1. The Data
   - Massive, operational and opportunistic
2. The Users and Sponsors
   - Business decision support
3. The Methodology
    - Computer-intensive
    - Multidisciplinary lineage

<br>

## `Trends leading to Data Flood`
### 데이터가 발생되는 곳
- 비즈니스
  + Web, e-commerce, transactions, stocks, bank, ...
- 과학
  + Remote sensing, bioinformatics, scientific simulation, ...
- 사회
  + news, digital cameras, ...

<br>

## `Definition of data mining`

| **분야**           | **정의**                           |
|:----------------:|:--------------------------------:|
| **컴퓨터과학자 그룹**    | 관계, 성향, 패턴 등의 정보를 찾아내는 과정        |
| **경영정보시스템(MIS)** | 의사결정, 지원시스템의 개발과정                |
| **통계학자 그룹**      | 데이터 분석 및 모형 선택 (model selection) |



<br>

## `데이터마이닝 도입 이유 및 단계`
1. 정보의 축적
2. 다차원 데이터
3. 정보처리 기술 발전
4. 데이터베이스, 데이터 웨어하우스 도입
5. CRM 도입 (Customer Relationship Management)

### **∴ Database -> Data Warehouse -> Data Mining**

<br>

## `Data Warehouse - 1`
### 주제지향성 (Subject Oriented)
Within any business, data naturally congregates around categoried or subject areas. Data warehouse are built around these broad, non-overlapping subjects rather than around a business process, system, or function. 
### 통합성 (Integrated)
Data is integrated by datawide consitencies in the measurement of variables naming conventions, and physical data definitions. 

### 시변성 (Time Variant) 
Historical and accurate at some point in time, data in a data warehouse is a "snapshot" of an organization's information. This archival and subsequent historical value gives data warehouses an element of time as part of their structure. 

### 비휘발성 (Non-volatile)
Since the data in the data warehouse is a snapshot of a corporation's data at a specific point in time, the data shouldn't be changed, modified, or updated. 


## `Data Warehouse - 2`
- 양질의 데이터 제공
- 시간 및 노력 절감
- 다양한 형태의 데이터 제공
- 데이터 지도 제공

## `Data Base vs. Data Warehouse`

| **-**    | **Data Base**                 | **Data Warehouse**         |
|:--------:|:-----------------------------:|:--------------------------:|
| **목적**   | 정확, 효율성을 통한 업무/거래처리           | 분석을 통한 전략수립/의사결정 지원        |
| **데이터**  | 휘발성, 지속적으로 갱신, 레코드 단위         | 시계열적, 읽기전용, 가공/요약된 데이터     |
| **형태**   | 업무단위(예: 대부, 저축, 신용)로 분리       | 주제별(예: 고객, 상품)로 통합         |
| **요구사항** | 데이터의 신속한 입력, 갱신, 추적, 데이터의 무결성 | 다량의 데이터를 다차원 분석, 응답시간의 최소화 |
| **사례**   | 예금입출, 대체                      | 상품수익률 분석, 우량고객 분류지원        |

<br>

## `OLAP (On-Line Analytical Processing)`
- DB나 DW에 정보 요구자가 직접 접근<br>
  -> 다차원적인 질의를 통해 대화식으로 정보를 탐색<br>
  -> 분석하고자 하는 관점에서 자료를 요약해주는 기법<br>

- 탐색적 목적의 정보 제공<br>
  -> 문제의 원인, 데이터간의 연관관계 등 새로운 지식 추출은 불가

### **∴ 현재 데이터로부터 사실에 대한 답을 얻는데 사용**

<br>

## `OLAP vs. Data Mining`
- OLAP
    + multi-dimensional analysis
    + 현재의 데이터 상황을 보여줌
- Data Mining
    + Flexible, nonparametric regression<br>
        (neural network, projection pursuit regression, polyclass)
    + OLAP보다 정밀, 정확, 패턴도 알려줌
    + 비모수회귀, 사영추적회귀 등