---
title: "데이터 분석 3일차 - 선형회귀 분석"
excerpt: "기본적인 선형 회귀 분석"

categories:
  - Deep Learning
tags:
  - Deep Learning
classes: wide
last_modified_at: 2021-07-29T07:31:00-05:00
---

> 미쳐야 미친다. 

***

# 데이터 분석 - 선형 회귀 분석 3일차 

### 단순 선형 회귀를 위한 OLS ( 최소 자승법 ) 계산

 단순 선형 회귀식은 y = α + βx 였음을 기억하자. 여기서의 목표는 비용 함수를 최소화하는 β 와 α 값을 찾는 것이다. β를 먼저 구해보자. β 계산을 위해서는 우선 x의 분산 및 x 와 y의 공분산을 계산해야 한다. 분산은 집합의 값들이 얼마나 산포됐는지를 보는 척도다.집합의 모든 수가 동일하면 분산은 0 이다. 분산이 작으면 숫자들이 평균 근처에 밀집해 있다는 듯이고, 평균으로부터 멀리 떨어질 수록 분산은 커진다. 
 

```python

import numpy as np

# X는 훈련데이터의 특징이고, 여기서는 피자의 지름이다.
# scikit-learn은 특징 벡터 이름을 X로 사용한다.
# 대문자는 행렬을 의미하고 소문자는 벡터를 의미한다.
X = np.array([[6], [8], [10], [14], [18]]).reshape(-1, 1)

x_bar = X.mean()

print(x_bar)

# 표본 분산을 계산할 때 훈련 인스턴스 개수로 부터 1을 차감하는 것에 주목하자.
# 이 기법은 베셀 교정(Bessel's correction)이라 불린다. 표본으로부터 모집단의
# 분산을 추정할 때 편향을 줄여준다.
variance = (( X - x_bar) ** 2).sum() / (X.shape[0] -1)
print(variance)

# NumPy는 분산을 계산하는 var 메소드를 제공한다. 키워드 변수 ddof를 사용해 베셀 교정을 이용해서 표본 분산을 계산하게 지정할 수 있다.
print(np.var(X, ddof=1))

# 공분산은 두 변수가 얼마나 함께 변화하는지 측정한다. 두 변수가 같이 증가한다면 공분산은 양수다. 한 변수가 증가할 때 다른 변수는 감소하면 공분산은 음수가 된다.
# 두 변수 사이의 선형 관계가 없다면 공분산은 0이 된다. 그러나 선현으로 상관되지 안았다고 해서 반드시 서로 독립적이라는 의미는 아니다.

y = np.array([7, 9, 13, 17.5, 18])
y_bar = y.mean();

# 두 벡터가 모두 행 벡터가 되야 하므로 X를 전치(transpose)한다.

covariance = np.multiply((X - x_bar).transpose(), y - y_bar).sum() / ( X.shape[0] - 1 )
print(covariance)
print(np.cov(X.transpose(), y)[0][1])

```

### Print에 대한 출력 결과 ( print 의 결과 ) 

![](https://keepinmindsh.github.io/lines/assets/img/dataanalysys_202108151.png){: .align-center} 


### 계산식 [ 참고 ]

![](https://keepinmindsh.github.io/lines/assets/img/dataanalysys_20210815.jpg){: .align-center} 


베셀 보정(Bessel’s Correction)이라고 하는데 왜 이렇게 해야 되냐? 보통 교과서나 강의들에서는 자유도 (degree of freedom)이라는 개념으로 설명합니다. 샘플링 한 표본들은 평균적으로 모집단 기댓값보다는 표본 기댓값에 더 가깝게 형성되어 있기 때문에 표본 분산 값은 모집단 분산 값보다 낮게 측정됩니다. 그거를 약간 조정하기 위해 N-1을 이용하여 표본 분산 값을 톡 쳐서 올려준다는 논리입니다.
{: .notice--info}

- 참조 : <https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=yunjh7024&logNo=220819925829> [제이의 블로그]
- 참조 : <https://learnshare.tistory.com/11> [Learn & Share :: Business and Data Note]
- 참조 : <https://www.youtube.com/watch?v=LZe94nm1lZg>