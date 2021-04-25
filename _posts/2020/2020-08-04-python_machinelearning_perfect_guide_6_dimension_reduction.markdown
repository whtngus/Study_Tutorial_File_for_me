---
layout: post
title: "python_machinelearning_perfect_guide 6_dimension_reduction"
date: 2020-08-04 19:20:23 +0900
category: book
---

# 차원 축소

## 01. 차원 축소(Dimension Reduction)개요

```
일반적으로 차원이 증가할수록 데이터 포인트 간의 거리가 기하급수적으로 멀어지게 되고,
희소(sparse)한 구조를 가지게 된다.
수백 개 이상의 피처로 구성된 경우 개별 피처간의 상관관계까 높을 가능성이 크다.
-> 이렇게 다차원의 피처를 차원 축소해 피처수를 줄일 수 있다면 직관적으로 데이터를 해석할 수 있다.

일반적으로 차원축소는 
피처 선택(feature selection)과
피처 추출(feature extraction)로 나눌 수 있다.

    - 피처 선택
특정 피처에 종속성이 강한 불필요한 피처는 아예 제거하고, 데이터의 특징을 잘 나타내는 주요 피처만 선택하는 것
    - 피처 추출
기존 피처를 저차원의 중요 피처로 압추개서 추출하는 것 
새롭게 추출된 중요 특성은 기존의 피처가 압축된 것이므로 기존 피처와는 완전히 다른 값이 된다.
ex) PCA, SVD, NMF 
```
# 02. PCA(Principal Component Analysis)

> PCA 개요

```
가장 대표적인 차원 축소 기법
여러 변수간에 존재하는 상관관계를 이요해 이를 대표하는 주성분(Principal Component)을 추출해 차원을 축소하는 기법
가장 높은 분산을 가지는 데이터의 축을 찾아 이 축으로 차원을 축소 (PCA의 주성분)

    - 방법
제일 먼저 가장 큰 데이터 변동성(Variance)을 기반으로 첫 번째 벡터 축을 생성
두 번째 축은 이 벡터 축에 지각이 되는 벡터를 축으로 한다.
세 번째 축을 다시 두 번째 축과 직각이 되는 벡터를 설정하는 방식으로 축을 생성
세 번째 축에 데이터를 정사영 시킴
```

## 03. LDA(Linear Discriminant Analysis)

```
선형 판별 분석법으로 불림
LDA는 지도학습의 분류에서 사용하기 쉽도록 개별 클래스를 분별할 수 있는 기준을 최대한 유지하면서 차원을 축소
클래스 간 분산을 최대화
클래스 내 분산을 최소화
```

## 04. SVD(Singular Value Decomposition)

```
SVD는 정방행렬뿐만 아니라 행과 열의 크기가 다른 행렬에도 적용할 수 있다.
    - SVD 강의 
https://www.youtube.com/watch?v=cq5qlYtnLoY
```

## 05. NMF(Non-Negative Matrix Factoriation)

```
Truncated SVD와 같이 낮은 랭크를 통한 행렬 근사(Low-Rank Approximation) 방식의 변형
원본 행렬 내의 모든 원소 값이 모두 양수라는 게 보장되면 다음과 같이 좀더 간단한 두개 기반 양수 행렬로 분해될 수 있는 기법
ex)
v(4*6) eq W(4*2)*H(2*6)

일반적으로 길고 가는행렬 W와 작고 넓은 행렬H로 분해한다.

분해 행렬 W는 원본 행에 대해서 잠재 요소의 값이 얼마나 되는지에 대응
분해 행렬 H는 잠재 요소가 원본 열(즉, 원본 속서)로 어떻게 구성됐는지를 나타내는 행렬
```

