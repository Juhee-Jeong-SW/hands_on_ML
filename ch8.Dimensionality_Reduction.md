# CH8. 차원 축소

## 8.2 차원 축소를 위한 접근 방법

1. 투영
2. 매니폴드 학습

### 8.2.1 투영

- 샘플들이 평면 상태로 존재함.

  → 3D에 존재하는 2D의 부분적인 공간

- 이 공간을 수직으로 투영하면 → 2D 데이터셋 얻음

⇒ 결과적으로 3D → 2D 로 차원이 축소된 것.

반드시 best는 아님

- 스위스롤 : 부분 공간이 뒤틀리거나 휘어 있는 상태
- 스위스롤을 펼쳐서 오른쪽과 같은 2D 데이터셋을 얻어야함. 왼쪽은 별로..

억지로 최적화해서 만들 수 있는 초평면에 투영하면 왼쪽과 같이 나온다. 하지만 우리가 얻어야 할 것은 펼쳐서 예쁘게 만들어야 함.

위의 예가 바로 2D 매니폴드

### 8.2.2 매니폴드 학습

즉, 2차원 초평면으로 보일 수 있는 3차원 공간 속의 일부로 판단할 수 있다는 것.

⇒ 펼쳐서 보거나 혹은 가까이서 보면 2차원 평면이지만 말려있기 떄문에 이 전체 공간의 크기인 3차원으로 보여지는 것이다.

정리하면,

d 차원 매니폴드는 국부적으로 d차원 초평면으로 보일 수 있는 n 차원의 일부이다.

- 많은 차원 축소 알고리즘은 이 매니폴드를 모델링하는 방식으로 작동함. ⇒ 매니폴드 학습
- 매니폴드 가정,가설 : 실제 고차원 데이터셋은 저차원 매니폴드에 가깝게 놓여있다.
- but, 이 가설이 항상 유효하진 않음.

![https://user-images.githubusercontent.com/37871541/50690457-b7f24400-1070-11e9-950d-22a1048390c8.png](https://user-images.githubusercontent.com/37871541/50690457-b7f24400-1070-11e9-950d-22a1048390c8.png)

1번 행일 것이라는 가정이다.

2번 행을 보면 아닐 수도 있다는 것을 알 수 있다.

## 8.3 PCA

- 차원 축소 알고리즘
- 데이터에 가장 가까운 초평면을 정의한 다음, 데이터를 이 평면에 투영시킴.

### 8.3.1 분산보존

![https://user-images.githubusercontent.com/37871541/50690644-6f875600-1071-11e9-907e-9e2292d9d8a3.png](https://user-images.githubusercontent.com/37871541/50690644-6f875600-1071-11e9-907e-9e2292d9d8a3.png)

- 왼쪽

  데이터 손실을 가장 줄이면서 저 데이터를 다 표현하려면 어떻게 해야할까? → c1선을 긋는 것이 좋을 것이다.

- 오른쪽

  실선 반점선 점선에 투영했으 때 데이터의 분포를 보여줌.

  가장 데이터 덩어리를 잘 표현하는 것은 C1

** 수치적으로 원래 덩어리의 데이터 손실량을 최소로 하는 선을 찾는 것. → (원래데이터 - 투영한 데이터) ^ 2 를 최소화하는 방향

### 8.3.2 주성분

분산이 최대인 축을 찾는다.

PCA가 말하는 것 : 데이터들을 정사영 시켜 차원을 낮춘다면, 어떤 벡터에 데이터들을 정사영 시켜야 원래의 데이터 구조를 제일 잘 유지할 수 있을까?

- 주성분

  이전의 두 축에 직교하는 세 번째 축을 찾으며 데이터셋에 있는 차원의 수만큼 네번째, 다섯번째,. n번째 축을 찾음→ i번째 축을 i번째 주성분이라고 함.

- 주성분 찾는 법? → SVD

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d194e978-c09f-4d4e-95a7-9196ab6168d2/_2021-01-27__6.54.05.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d194e978-c09f-4d4e-95a7-9196ab6168d2/_2021-01-27__6.54.05.png)

### 8.3.3 d차원으로 투영하기

- 주성분 모두 추출했으면 처음 d개의 주성분으로 정의한 초평면에 투영하여 데이터셋을 d 차원으로 축소시킬 수 있음.
- 초평면 : 가능한 분산 큰 것.

### 8.3.4 사이킷런 사용하기

- 사용하는 것...

### 8.3.5 설명된 분산의 비율

- 유용 정보 중 하나..
- 각 주성분의 축을 따라 존재하는 데이터셋의 분산 비율을 나타냄

### 8.3.6 적절한 차원 수 선택하기

- 임의로 정하기 보단 적절한 분산이 될 때까지 더해야 할 차원 수를 선택하는 것이 간단함
- 차원을 축소하지 않고 PCA를 계산한 뒤 , 훈련 세트의 분산으 95%로 유지하는 데 필요한 최소한의 차원 수를 계산
- or 함수로 그리기...

### 8.3.7 압축을 위한 PCA

- 압춘된 데이터셋에 PCA 투영 변환을 반대로 적용해 다시 되돌릴 수 있음.
- 완벽하진 않지만 매우 비슷할 것.
- (원본 데이터 - 재구성데이터의 평균)^2 ⇒ 재구성 오차

### 8.3.8 랜덤 PCA

- 랜덤 pca 는 확률 알고리즘 활용 → 처음 d개의 주성분에 대한 근사값을 빠르게 찾음.
- d가 n보다 많이 작다면 svd보다 훨씬 빠름.

### 8.3.9 점진적 PCA

- 점진적은 훈련 세트를 미니배치로 나눈 뒤 IPCA 알고리즘에 한 번에 하나씩 주입하는 것..
- 훈련세트가 클 때 유용함!

## 8.4 커널 PCA

앞에서 배운 커널 트릭 여기서도 적용해보자.

- 차원 축소를 위한 복잡한 비선형 투영을 수행할 수 있음. ⇒ 커널 PCA

### 8.4.1 커널 선택 및 하이퍼 파라미터 튜닝

- 종종 지도학습의 전처리 단계로 활용됨 → 그리드 탐색으로 성능 가장 좋은 커널과 하이퍼 파라미터 선택 가능
- kPCA를 사용해 차원을 2차원으로 축소 → 분류를 위한 로지스틱 회귀를 적용
- 가장 높은 분류 정확도를 얻기위 해 GridSearchCV를 사용해 얻는다.

재구성 원상 → 특성 공간은 무한 차원이기 때문에 재구성된 포인트를 계산할 수 없고, 재구성에 따른 실제 에러를 계산할 수 없다. 하지만 재구성된 포인트에 가깝게 매핑된 원본 공간의 포인트를 찾을 수 있다. 이게 재구성 원상

투영된 샘플로 훈련 세트로, 원본 샘플을 타깃으로 하는 지도 학습 회귀 모델을 훈련 시키는 것.