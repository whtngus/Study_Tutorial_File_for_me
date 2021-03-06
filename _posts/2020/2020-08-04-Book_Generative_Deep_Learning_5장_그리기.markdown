---
layout: post
title: "Book_Generative_Deep_Learning 5장 그리기"
date: 2020-08-04 19:20:23 +0900
category: book
---

# 5장 그리기

## 스타일 트랜스퍼(Style transfer)
```
    - 스타일 트랜스퍼
주된 먹적은 스타일 이미지(Style Image)가 주어졌을 때 같은 분류에 속한 것 같은 느낌을 주도록
베이스 이미지(base image)를 변환하는 모델을 훈련하는 것
스타일 트랜스퍼는 스타일 이미지에 내제된 분포를 모델링하는 것이 아니라 이미지에서 스타일을 결정하는 요소만을 
추출하여 베이스 이미지에 주입하는 것
```

## CycleGan

> CycleGan(cycle-consistent adversarial network)

```
이 논문은 스타일 트랜스퍼 분야에서 큰 진전을 이루어 낸것으로 평가를 받는다.
샘플 쌍으로 구성된 훈련 세트 없이도 참조 이미지 세트의 스타일을 다른 이미지로 복사하는 모델을 만듦

CycleGAN 논문에서는 아티스트-사진 스타일 트랜스퍼에 대한 최상의 결과를 얻기 위해 200번의 에폭 동안 모델을 훈련
```

> 뉴럴 스타일 트랜스퍼(neural style transfer)

```
다른 종류의 스타일 트랜스퍼 애플리케이션
룬션세트를 사용하지 않고 이미지의 스타일을 다른 이미지로 전달
```

## 손실함수

```
    - 손실함수
아래 3개의손힐 함수의 가중치 압을 기반으로 작동
1. 콘텐츠 손실(content loss)
합성된 이미지는 베이스 이미지의 콘텐츠를 동일하게 포함해야 한다.
2. 스타일 손실(style loss)
합성된 이미지는 스타일 이미지와 동일한 일반적인 스타일을 가져야 한다.
3. 총 변위 손실(total variation loss)
합성된 이미지는 피셀처럼 격자 문늬가 나타나지 않고 부드러워야 한다.

경사 하강법으로 위 손실을 최소화 한다.
```

> 콘텐츠 손실

```
내용과 전반적인 사물의 배치 측면에서 두 이미지가 얼마나 다른지를 측정 

콘텐츠 손실은 개별 픽셀값과 무관해야 한다. 
-> 두 이미지의 장면이 같더라도 개별 픽셀값이 비슷할 것으로 기대할 수 없기 때문에
=> 대락적인 위치를 기반으로 이미지를 점수화
따라서 이미지의 내용을 식별하도록 성공적으로 훈련된 심층 신경망이 필요
    - 결론 
베이스 이미지와 현재 합성된 이미지에 대해 이 출력을 계산하여 그사이의 평균 제곱 오차를 측정하한 값이 
콘텐츠 손실 함수이다.
논문에서는 VGG19를 사용 
```

> 스타일 손실

```
스타일이 비슷한 이미지는 특정 층의 특성 맵사이에 동일한 상관관계(correlation)패턴을 가진다는 아이디어를 기반으로한다.
ex)
VGG19 네트워크의 어떤 층에서 한 채널은 녹색을 감지 , 다른 채널은 뾰족함을 감지, 마지막 채널은 갈색 부분을감지
같은 잔디에대해서 특성맵이 겹치는 부분이 많아짐

이러한 방법을 이용하여 특성 맵을 폋리고 스칼라곱(scalar product) or 접곱(dot product)를 계산.
계산 값이 크면 특성 맵 사이의 상관관계가 크고, 값이 작으면 특성 맵 사이의 상관관계가 없다.
 
    - 그람 행렬(Gram matrix)
층에 있는 모든 특성 사이의 스칼라곱을 담은 행렬을 정의

```

> 총 변위 손실

```
단순히 합성된 이미지에 있는 잡읍을 측정 
오른쪽으로 한 픽세을 이도하고 원본 이미지와 이동한 이미지 간의 차이를 제곱하여 더한다.
아래로도 이동하여 측정
```



















