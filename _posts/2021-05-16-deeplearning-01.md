---
title: "Deep Learning"
excerpt: "기본적인 개념에 대해서"

categories:
  - Deep Learning
tags:
  - Deep Learning
classes: wide
last_modified_at: 2019-05-16T16:00:00-05:00
---

> 이루어야할 게 생긴다면, 그냥 하는 거지. 고민 따위 의미 없다.  


***

# 모든 머신 러닝 알고리즘은 컴퓨터 프로그램을 작성해서 구현됩니다. 
- 제일원리
철학에서 제일원리(First principle)는 기초적이고 근원적인 가정 또는 제안을 의미하며, 이는 다른 가정 또는 제안에서 유도될 수 없다. 수학에서 제일 원리는 공리로 언급된다.
제일원리의 고전 적인 예로 유클리드의 기하학에 사용된 공리가 있다. 유클리드 기하학의 수백가지 명제들은 세 종류의 제일원리에 의해서 모두 유도가 가능하다. 여기서 세 종류의 제일원리는 유클리드 기하학에서 가정한 정의(definitions), 공준(postulates), 통념(common notions)에 해당한다.
자연과학에서는 제일원리를 그리스 원어인 Ab Initio 또는 풀어서 제1원리 계산으로 주로 사용한다.

# 머신러닝 

**정해진 행동에 대한 코드를 만드는 것이 아닌, 더 많은 경험을 하면 능력이 향상되는 프로그램을 디자인하는 것입니다.**  
예 : 지도학습

### 머신러닝을 위한 기본 자료 
- 데이터 
  - 이미지, 텍스트, 오디오, 비디오
- 데이터를 어떻게 변환할지에 대한 모델
  - 딥러닝 
- 우리가 얼마나 잘하고 있는 지를 측정하는 loss 함수 
  - 우리의 모델이 얼마나 잘하고 있는 지를 평가하기 위해서 모델의 결과와 정답을 비교할 필요가 있음 
  - 우리의 결과가 얼마나 나쁜지를 측정하는 방법을 제공 - Loss 함수 
  - 이 파라미터 들의 가장 좋은 값은 관찰된 데이터의 학습 데이터에 대한 loss를 최소화하는 것을 통해서 "배우"기를 원한다는 것
    - 학습 오류
    - 테스트 오류 
- loss 함수를 최소화할 수 있도록 모델 파라미터를 바꾸는 알고리즘 
- 최적화 알고리즘 
  - loss를 최소화 하기 위해서 모델와 loss 함수를 최소화하는 파라미터 집합을 찾는 방법이 필요함. 

### 지도학습

- y : 레이블 - 타겟
- x : 샘플/인스턴스 - 입력 데이터 포인트 
- 지도학습은 주어진 데이터에 대한 타켓을 예측하는 문제를 푸는 것입니다. 
- 타켓은 종종 레이블이라고 불리고, 기호로는 y로 표기합니다. 입력 데이터 포인트는 sample 또는 인스턴스라고 불리기도 하고, x로 표기됩니다. 
- 입력 x 를 예측 on fθ(x) 로 매핑하는 모델 fθ를 생성하는 것이 목표입니다. 

예를 들면, 여러분이 의료분야에서 일한다면, 어떤 환자에게 심장마비가 일어날 지 여부를 예측하기를 원할 것입니다. 이 관찰, 심장 마비 또는 정상, 은 우리의 레이블 y가 됩니다. 
입력 x는 심박동, 이완기 및 수축 혈압 등 바이탈 사인이 될 것입니다. 파라미터 θ(세타)를 선택하는 데, 우리는 레이블이 있는 예들, xi, yi 을 모델에게 제공하기 때문에 감독이 작동합니다, 이때 xi는 정확한 레이블과 매치되어 있습니다. 

확률용어로는 조건부 확률을 추정하는데 관심이 있습니다. 지도학습은 실제로 사용되는 머신 러닝 대부분을 설명합니다. 부분적으로, 많은 중요한 작업들이 몇 가지 이용 가능한 증거가 주어졌을 때. 알 수 없는 것의 확률를 추정하는 것으로 설명될 수 있기 때문입니다.

- 이번 달의 제정 보고 데이터를 기반으로 다음달 주식 가격을 예측하기 

'입력으로 부터 타겟을 예측한다'라고 간단하게 설명했지만. 지도학습은 입력과 출력의 타입, 크기 및 개수에 따라서 아주 다양한 형식이 있고 다양한 모델링을 요구합니다. 예를 들면, 텍스트의 문자열 또는 시계열 데이터와 같은 시퀀스를 
처리하는 것과 고정된 백터 표현을 처리하는데 다른 모델을 사용합니다. 

###### 시계열 데이터란?

시계열(time series) 데이터는 관측치가 시간적 순서를 가진 데이터로, 변수간의 상관성(correation)이 존재하는 데이터를 다루며, 연속(continous)하거나 불규칙적(irregular)데이터는 다루지 않는다.
시계열 데이터는 과거의 데이터를 통해서 현재의 움직임 그리고 미래를 예측하는데 사용된다. 일반적인 label데이터는 input과 label간의 상관관계를 다루는 반면에 시간에 따라 어떻게 움직이는 과거의 자료를 가지고 예측하게 된다.  

![](https://keepinmindsh.github.io/lines/assets/img/timeseries.png){: .align-center} 

- 추세 : 추세라는 것은 말 그대로 경향을 의미한다. 세부적인 데이터를 다 빼고 전체적으로 보았을 때 주식이 감소하는지 증가하는지 대략적인정보를 보여준다.

- 계절성 : 특정한 기간마다 어떤 패턴을 가지고 반복하는지 확인 할 수 있는 특성이다. 이 데이터를 통해 앞으로 어떻게 변화할 것인지 예측할 수 있다.

- 랜덤 : 노이즈(noise)라고도 불리는 이 데이터는 추세, 계절성 등으로 설명되지 않은 데이터를 의미한다. 이러한 데이터를 가지고 예측하게 된다면 예측의 오차가 커지기 때문에 전처리를 통해서 최대한 예측하는데 관여하지 않도록 하는 것이 중요하다.

시계열 분석의 토대가 되는 방법론에 대해서 살펴보면 기본적으로 우리는 예측을 하기 위해서 A 변수로 ( 독립변수 ) 로 B 변수 ( 종속변수 )를 예측한다. 시계열 변수 만의 남다른 특징은 위의 과정에서 시계열 데이터가 추가되는 것이다.   
시계열 데이터는 정상 시계역과 비정상 시계열로 나뉜다.  

- 정상 시계열 

 뚜렷한 추세가 없고 진폭이 시간의 흐름에 따라 일정한 것을 의미한다. 

- 비정상 시계열 

 시간대에 따라 데이터가 변하고 추세와 시간대를 갖는 것을 의미한다.   


 우리가 진행할 시게열 분석의 모형으로 쓰이는 대부분 알고리즘은 정상 시계열을 원한다. 그래서 데이터가 비정상 시계열일 경우, 정상 시계열로의 변환이 필요하다.  
최종적으로 쓰이는 형태는 p,d,q이며, p,d,q는 우리가 설정해야하는 모수이다. 


### 시계열 데이터 분석 

###### 시계열 분석을 위한 수리적 모형 ARIMA

- ARIMA

 자기회귀모형(AutoRegression)과 이동평균모형(MovingAverage)가 결합된(Intergrated) 모형이다. => AR + I + MA

 ```python

# 시계열 데이터 분석 1차 

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# ARIMA 모형이 인식할 수 있는 series 데이터 형태로 호출해야함. 
data_ARIMA = pd.Series.from_csv('/Users/apple/Desktop/air_passengers.csv', sep=';', header=0, parse_dates=True)
data_ARIMA.head(5)

# Indexing 처리 
data_ARIMA_cut = data_ARIMA.iloc[0:132, ]
data_ARIMA_cut.tail()

data_ARIMA_cut_float = data_ARIMA_cut[:].astype(np.float)
data_ARIMA_cut_float.tail()

data_ARIMA_cut_float.plot()
plt.show()

 ```

- p, q에 대한 판단 

```python

import metaplotlib.pyplot as plt 
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf 

plot_acf(data_ARIMA_cut_float)
plot_pacf(data_ARIMA_cut_float)
pit.figure(figsize=(20,4))
plt.show()

```

- 차분횟수 d 구하기 

```python

diff_1 = data_ARIMA_cut_float.diff(periods=1).iloc[1:]
diff_1.plot()
plot_acf(diff_1)
plot_pacf(diff_1)
plt.show()

```

- 차분 횟수와 ARIMA의 모수를 이용한 적용 

```python

from statsmodels.tsa.arima_model import ARIMA
from statsmodels.tas.arima_model import ARIMAResults

model = ARIMA(data_ARIMA_cut_float, order=(1,1,0))
model_fit = model.fit(trend='nc', full_output = True, disp = 1 )
print(model_fit.summary())


model_fit.plot_predit()

fore = model_fit.forecast(steps = 1)
print(fore)

```


- Deprecated since version 0.21.0: Use pandas.read_csv() instead.

https://pandas.pydata.org/pandas-docs/version/0.23/generated/pandas.Series.from_csv.html => Link 참고 

- MA, Prophet, AR, A 

https://www.kaggle.com/bogdanbaraban/ma-prophet-ar-arma-arima-lstm

- 시계열 샘플 데이터 

https://github.com/dacatay/time-series-analysis/tree/master/data



### 지도학습의 과정

예제 입력을 많이 수집해서, 임의로 고릅니다. 각각에 대해서 ground truth 를 얻습니다. 입력과 해당하는 레이블을 합쳐서 학습데이터를 구성합니다. 학습 데이터를 지도학습 알고리즘에 입력합니다.
여기서 지도학습 알고리즘은 데이터셋을 입력으로 받아서 어떤 함수를 결과로 내는 함수입니다. 그렇게 얻어진 학습된 모델을 이용해서 이전에 보지 않은 새로운 입력에 대해서 해당하는 레이블을 측정합니다. 

### 회귀(regression)

**지도학습 : 회귀**  

 주택 판매 데이터베이스에서 추출된 데이터를 예로 들어보겠습니다. 각 행은 하나의 집을, 각 열은 관련된 속성을 갖는 테이블을 만듭니다. 우리는 이 데이터 셋의 하나의 행을 속성 벡터라고 부르고, 이와 관련된 객체는 예제라고 부릅니다.  

만약 여러분이 뉴욕이나 샌프란시스코에서 살고, 아마존, 구글, 마이크로소프트, 페이스북의 CEO가 아니라면 , 여러분 집의 속성 벡터(집 면적, 침실수, 화장실수, 도심까지 도보거리)는 아마도 [100, 0, 0.5, 60] 가 될 것입니다. 하지만,
피츠버그에 산다면 [3000, 4, 3, 10]와 가까울 것입니다. 이런 속성 벡터는 모든 전통적인 머신러닝 문제에 필수적인 것입니다. 우리는 일반적으로 어떤 예제에 대한 속성 백터를 xi로 표기하고, 모든 예제에 대한 속성 벡터의 집합을 X로 표기합니다. 

결과에 따라서 어떤 문제가 회귀(regression)인지를 결정됩니다. 새 집을 사기 위해서 부동산을 돌아다니고 있다면, 여러분은 주어진 속성에 대해서 합당한 집 가격을 추정하기를 원합니다. 타겟 값, 판매가격, 은 실제 숫자가 됩니다.   
타겟 값, 판매 가격,은 실제 숫자가 됩니다. 샘플 xi에 대응하는 각 타겟은 yi로 표시하고, 모든 예제 X에 대한 모든 타켓을 y로 적습니다. 타겟이 어떤 범위에 속하는 임의의 실수 값을 갖는 다면, 우리는 이를 회귀 문제라고 부릅니다. 우리의 모델의 목표는 실제 타겟값을 근접하게 추정하는 예측을 생성하는 것입니다. 이 예측을 yi 로 표기합니다. 

- 이 수술은 몇 시간이 걸릴가요? - 회귀
- 이 사진에 개가 몇마리가 있나요? - 회귀

그런데 만약 주어진 문제에 대한 질문을 "이것은 ... 인가요?"라고 쉽게 바꿀 수 있다면, 이것은 분류의 문제입니다.   


*참조 링크* : https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=makeydrew&logNo=221400031097

