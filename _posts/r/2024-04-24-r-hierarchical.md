---
layout: single
title: "Hierarchical Clustering in R"
categories: R
tag: [datamining, machine-learning, hierarchical-clustering, unsupervised-learning, r]
toc: true # 목차 보여주기
author_profile: false   # 프로필 제거
# sidebar:    # 프로필 제거 후 사이드바 보여주기
#     nav: "counts"
typora-root-url: ../
---
<br>

# **※ Hierarchical Clustering in R (계층적 군집분석)**

## ■ 유사도 행렬 생성
- parameter
  - method : 거리 측정 방식 ("euclidean" / "maximum" / "manhattan" / "canberra" / "binary" / "minkowski" 등)

```r
> dist(data, method)
```

<br>

## ■ 군집 구성
- parameter
  - method : 군집 구성 방법 ("single" / "complete" / "average" / "centroid" / "ward.D2" 등)

```r
> hclust(data, method)
```

```r
> df.dist <- dist(data, method = "euclidean")

> hclust(df.dist, method = "single")
> hclust(df.dist, method = "complete")
> hclust(df.dist, method = "average")
> hclust(df.dist, method = "centroid")
> hclust(df.dist, method = "ward.D2")
```

<br>

## ■ dendrogram 생성 & 군집 시각화
- plot
  - dendrogram 생성
  - parameter
    - cex : 글자 크기
    - hang : -1로 하면 줄기가 바닥에서 나오게 설정가능
- rect.hclust
  - 군집간 경계를 그려, 군집이 어떻게 나뉘는지 확인가능
  - parameter
    - k : 군집 개수
    - border : 경계선 색깔

```r
> df.hclust <- hclust(df.dist, method = "single")

> plot(df.hclust, cex = 0.6, hang = -1)
> rect.hclust(df.hclust, k = 4, border = 2:5)
```

<br>

## ■ raw data에 cluster 할당

```r
> cutree(data, k)
```
```r
> df.clusters <- cutree(df.hclust, k = 4)
> data$cluster <- df.clusters
```

<br>

## ■ 2차원 시각화

```r
> fviz_cluster()
```
