# 1. 경사하강법(Gradient Descent)


모델은 “어떻게” 학습하는가 에서의 “**어떻게**” 파트. 
앞에서 구한 cost function 을 바탕으로 오차를 줄여나가는 방식으로 parameter 를 업데이트하게 되는데, 그에 대한 방식이 바로 Gradient Descent 입니다.

많은 책이나 강의에서 Gradient Descent 에 대해 설명할 때 이렇게 설명합니다.

> 짙은 안개 때문에 산속에서 길을 잃었다고 생각해보세요. 발밑 지면의 기울기만 느낄 수 있습니다. 빨리 골짜기로 내려가는 좋은 방법은 가장 가파른 길을 따라 아래로 내려가는 것입니다. 이것이 바로 경사 하강법의 원리입니다.


> 

**결국 Gradient Descent 는 “어느 방향으로 갈 것인가” 를 결정하는 것**

Remind
경사하강법의 ‘학습한다’라는 것은 ‘오차의 최솟값을 찾아나간다’라는 의미

## 경사하강법의 문제점

### Local Minima 문제

모든 cost function 이 하나의 최솟값을 가지는 매끈한 곡선 형태는 아닙니다. 두 번째 그래프의 경우 알고리즘이 왼쪽에서 시작하게 되면 global minimum 이 아닌, local minimum 에 도달하게 됩니다.

다행히 MSE, RMSE와 같은 cost function에서는 함수가 convex function이라는 것이 증명되었지만, 아닌 경우에는 주의해야 합니다.

특히 deep learning의 경우 cost function이 정확히 어떤 모양인지 예측할 수 없어서 local minimum에 빠지는 경우를 주의해야 하며, local minimum을 탈출하는 방법에 대해 **여러 알고리즘**이 존재합니다.

# 규제선형모델

## 규제선형모델의 개요

- **등장 배경**

모델이 훈련세트에 과대적합되지않도록 ‘규제’를 가하고자 등장한 모델

    ```좋은 머신러닝 회귀 모델 = 적절히 데이터에 적합하면서도 회귀 계수가 기하급수적으로 커지는 것 제어 가능 해야함
    + 비용함수 : 학습 데이터의 잔차 오류 값을 최소화하는 RSS 최소화 방법, 과적합 방지를 위한 회귀 계수 값 크지 않도록 해야함 ```


→ 선형 회귀 모델에서는 특성에 곱해지는 계수(기울기)의 크기를 조정


## 규제 선형 모델의 종류

### 1) 릿지 회귀

‘**계수를 제곱한 기준**’으로 규제를 적용 (L2 규제)


### 2) 라쏘 회귀

‘**계수의 절댓값 기준**’으로 규제를 적용 (L1 규제)

### 3) 릿지와 라쏘의 비교
 - 모두 계수의 크기를 줄이지만 라쏘는 0으로 만들기가 가능함.
 - 라쏘 모형 : 유용한 특성을 골라내는 용도로 사용

 ### 4) 엘라스티겟 회귀
  L2와 L1 규제를 결합한 회귀

**등장 배경**
라쏘 회귀 : 서로 상관관계가 높은 피터들의 경우에 이들 중 중요 피처만 선택, 다른 피처들 모두 회귀 계수 0으로 만드는 성향 강함
-> 회귀 계수의 값이 급격히 변동할 수 있음

이를 완화하기 위해 L2 규제를 Lasso 회귀에 추가

# 스케일링
## 스케일링이란
- 데이터 전처리 과정 중 하나로, 모든 피쳐들의 데이터 분포나 범위를 동일하게 조정하는 과정

- 피쳐별로 데이터의 범위가 다르면 피쳐를 비교하기가 어려워 머신러닝이 잘 작동하지 않을 수 있다. 모든 특성의 범위(분포)를 같게 만들어 잘 작동할 수 있도록 만드는 과정을 의미


### 주요 개념
표준화 : 입력된 값의 정규 분포를 평균이 0이고 분산이 1인 표준 정규 분포로 변환하는 것

정규화 : 입력된 x 값들을 모두 0과 1 사이의 값으로 변환해 서로 다른 피쳐의 크기를 통일하는 개념

## 스케일링 변환 시 주의사항

- 사이킷런(Scikit-Learn)  :  sciPy와 Toolkit을 합친 파이썬 기반 머신러닝용 라이브러리

- 학습 데이터(Training Data)  :  모델이 학습하는 데 사용되는 데이터
- 테스트 데이터(Test Data)  :  모델이 학습된 후에 모델의 성능을 검증하기 위해 사용되는 데이터
   
   ```- 전체 데이터 셋을 학습 데이터와 테스트 데이터로 분할하는 것이 일반적이다. 예를 들어, 전체 데이터 셋 중 70%를 학습 데이터로 사용하고, 나머지 30%를 테스트 데이터로 사용하는 것이 일반적인 분할 비율```

### 스케일링 종류

### A. StandardScaler()

- 특성(feature)의 평균을 0, 분산을 1로 맞추는 표준화(Standardization)를 수행

- 선형 모델이나 신경망과 같은 알고리즘에서 잘 작동한다는 특징이 있다.
- 회귀보다 분류에 유용하다.

### B. MinMaxScaler()

- 모든 피쳐들이 0과 1사이의 데이터 값을 갖도록 변환
- 데이터의 최소값과 최대값을 알 때 사용
- 분류보다 회귀에 유용

### C. MaxAbsScaler()
- 데이터가 -1과 1 사이에 위치하도록 스케일링
- 절대값의 최소값이 0, 절대값의 최대값이 1이 되도록 스케일링
- 큰 이상치에 민감

### D. RobustScaler()

- 데이터의 중앙값이 0, IQE(Q3-Q1) = 1이 되도록 스케일링
  
- StandardScaler와 비슷, RobustScaler는 중간값과 사분위값, StandardScaler는 평균과 분산을 사용

### E.Normalizer()

- 각 데이터 포인트(행)의 norm(크기)을 1로 만들어주는 스케일링 방법

- 앞의 4가지 방법은 각 피처의 통계치를 이용, 즉 열을 대상으로 스케일링

- Normalizer() 의 경우 각 행마다 정규화가 진행

# 4. 차원 축소


- 차원은 수학에서 공간 내에 있는 점 등의 위치를 나타내기 위해 필요한 축의 개수

```
주성분 분석 PCA: 고차원 데이터를 기존의 분산을 최대한 보존하는 선형 독립의 새로운 변수들로 변환: 여러 변수 간에 존재하는 상관관계를 이용해 이를 대표하는 주성분을 추출해 차원 축소


SVD는 정사각행렬이 아닌 m*n 형태의 다양한 행렬을 분해하며, 이를 특이값 분해

NMF : 하나의 객체정보를 음수를 포함하지 않은 두 개의 부분 정보로 인수분해하는 방법
```

### 차원 축소 해야하는 이유

1. 차원이 커지면서 두 데이터간의 거리가 멀어지고 밀도가 급격히 줄어들기 때문에 차원을 축소해야한다.

2. 고차원 문제를 풀다보면 너무 정교해서 일반화가 힘들다.

3. 데이터가 낮은 차원에서 분석하는 것이 구조를 파악하는데 용이하다.
