# #Contents_of_Statistics
* [신뢰구간, p 값의 의미 - #1](#1)
* [중심극한정리의 의미 - #2](#2)
* [샘플링 (Sampling), 리샘플링 (Resampling)의 의미 - #3](#3)
* [가능도 (Likelihiood), 확률 (Probability)의 의미 - #4](#4)
---

## #1 
### 신뢰구간과 p 값의 의미 

- **모수 (Parameter)**
  - 평균, 분산과 같이 모집단의 특성을 보여주는 고정된 값 

<br>

- **신뢰수준 (Confidence Level)**
  - 표본 통계량 및 신뢰구간에 모수가 포함될 확률 
  - **EX)** 신뢰수준 95% => 동일 방법으로 100번의 표본 추출 중 95번은 모수를 포함

<br>

- **신뢰구간 (Confidence Interval)**
  - 모집단의 모수 (Parameter)가 위치해 있을 것으로 신뢰할 수 있는 구간 
  - 모수가 어느 범위 안에 있는지를 확률적으로 보여주는 방법
  - 주어진 신뢰수준에서 모수를 포함할 것으로 예상되는 구간 

<br>

- **유의확률 (p-value, Probability Value)**
  - 귀무가설이 진실이라는 가정에서 표본 통계량 값이 관측될 확률 
  - 귀무가설이 맞다고 가정할 때 얻은 결과보다 극단적인 결과가 실제로 관측될 확률 

<br>

- **유의수준 (Significance Level)**
  - 통계적 가설검정에서 귀무가설을 기각하는 확률의 최댓값
  - **EX)** 표본 평균이 모평균과 같을 때, 표본 평균이 모평균과 다르다고 선택하는 오류를 범할 확률의 혀용 한계

<br>

***REF***
- [공돌이의 수학정리노트 - 신뢰구간의 의미](https://angeloyeo.github.io/2021/01/05/confidence_interval.html)
- [공부하는 떡볶이 - 신회구간과 신뢰수준](https://ddukbbok-kang.tistory.com/84)

</br>

[BACK TO HEAD](#Contents_of_Statistics)

---

## #2
### 중심극한정리 (Central Limit Theorem)
- 동일한 확률분포를 가진 **'독립' 확률 변수 n개의 평균의 분포**는 n이 적당히 크다면 정규분포에 가까워진다는 정리
  - 일반적으로 표본의 크기가 30 이상일 때, 중심극한정리가 적용된다고 할 수 있음
  
  
- $[X_1, \ldots, X_n]$ 을 평균 $\mu$, 분산 $\sigma^2$인 분포에서 추출한 확률표본의 집합이라고 할 때, 
  
  - $$E(\bar{X}) = E(\frac{1}{n}(X_1 + \ldots + X_n)) = \frac{1}{n}(E(X_1) + \ldots + E(X_n)) = \frac{1}{n} * (n * \mu) = \mu$$

  - $$Var(\bar{X}) = Var(\frac{1}{n}(X_1 + \ldots + X_n)) = \frac{1}{n^2}(Var(X_1) + \ldots + Var(X_n)) = \frac{1}{n^2} * (n*\sigma^2) = \frac{\sigma^2}{n}$$

  - $$\bar{X} \sim N(\mu, (\frac{\sigma}{\sqrt n})^2) => Y = \frac{\sqrt{n}(\bar{X} - \mu) }{\sigma} = \frac {(\bar X - \mu) }{\sigma\sqrt{n}} \sim N(0, 1)$$ 

  
- 모집단 $X_j$에 대해 추가적인 정보 없이 평균 $\mu$와 분산 $\sigma^2$만 정의된다면 </br> 
  => 중심극한정리를 통해 **표본평균의 분포가 평균 $\mu$ 와 분산 $(\frac{\sigma}{\sqrt{n}})^2$인 정규분포에 근사한다**는 것을 알 수 있음 </br>
  => **표본 통계량을 통해 모수를 추정**할 수 있는 수학적 근거를 제시함

<br>

***REF***
- [중심 극한 정리](https://ko.wikipedia.org/wiki/%EC%A4%91%EC%8B%AC_%EA%B7%B9%ED%95%9C_%EC%A0%95%EB%A6%AC)
- [중심극한정리와 정규성검증](https://speedspeed.tistory.com/202#google_vignette)
- [수리통계 - 중심극한정리](https://www.goteodata.kr/77)
- [중심 극한 정리(CLT)](https://gguguk.github.io/posts/CLT/)

</br>

[BACK TO HEAD](#Contents_of_Statistics)

--- 

## #3
### 샘플링 (Sampling), 리샘플링 (Resampling)의 의미 
- **샘플링 (Sampling)**
  - 전체 데이터 집단 (**모집단**)에서 임의의 데이터를 일부 추출 (**표본 집단**)
  - 모집단 전체에 대한 조사가 사실상 불가능하기 때문에 샘플링을 이용 </br>
    => 표본 집단에 대한 조사를 통해 모집단에 대한 추론을 진행 
  - 선택 편향과 샘플링 오류와 같이 오류가 발생할 수 있음 </br>
    => 추론한 모집단의 특성에 필연적으로 영향을 끼친다
  
  - 종류 
    - **단순 무작위 추출 (Simple Random Sampling)**
      - 모집단의 모든 데이터를 동등한 확률을 통해 표본 추출 
      - 가장 단순한 표본 추출 방법
    
    - **층화 임의 추출 (Stratified Random Sampling)**
      - 전체 모집단을 몇 개의 특징을 기준으로 계층으로 나눈 뒤, 각 계층에서 독립적으로 표본을 추출
      - 계층 간 이질적, 계층 내 동질적 
    
    - **군집 추출 (Clustering Sampling)**
    - 전체 모집단을 모집단과 유사한 특성을 가진 여러 개의 군집으로 나눈 뒤, 선정된 군집에서 표본을 추출 
    - 군집 간 동질적, 군집 내 이질적 특성을 가짐
  - 
    - **계통 추출 (Systematic Sampling)**
      - 추출 간격을 정해 각 순서에 위치한 단위들을 표본으로 추출 
      - 난수 발생을 통해 단순 무작위 추출을 적용하기 어려운 상황에서 활용 

</br>
  
- **리샘플링 (Resampling)**
  - 기존의 샘플링한 표본 집단을에서 새로운 표본 집단을 다시 샘플링하는 과정 

  - 종류
    - **교차검증 (Cross-Validation)**
      - 모델 학습시 데이터를 훈련용, 검증용으로 교차하여 선택하여 학습을 진행
        - LpOCV (Leave_P_Out_CV), LOOCV (Leave_One_Out_CV)
        - K-Fold CV
        - Bias-Variance Trade-off for 
    - **Bootstrap**
      - 모집단에서 독립적인 데이터셋을 반복해 얻는 대신 원래의 데이터셋으로부터 중복을 허용해 관측치를 반복적으로 추출 

</br>

***REF***
- [샘플링(Sampling) 과 리샘플링(Resampling)](https://ploradoaa.tistory.com/81)
- [갈아먹는 통계 기초[3] - 표본 추출](https://blog.firstpenguine.school/35)
- [머신러닝 ISL 05 : Resampling Methods](https://m.blog.naver.com/parksoungpark/223054214575)
- [[머신러닝] 교차검증(Cross-validation) 필요성 및 장단점](https://heytech.tistory.com/113)

</br>

[BACK TO HEAD](#Contents_of_Statistics)

---

## #4
### 가능도 (Likelihiood), 확률 (Probability)

- **확률 (Probability)**
  - 특정 결과가 발생할 가능성 혹은 기회
  - 모델 매개변수에 따라 예측한 특정 결과의 발생 가능성을 의미 
  - '주어진 확률분포가 고정된 상태'에서 관측되는 사건이 변화될 때의 확률
  
- **가능도 (Likelihood)**
  - 모델이나 가설이 관찰된 데이터에 얼마나 잘 맞는지를 나타내는 정량적 추정 또는 측정 
  - 특정 매개변수 집합에서 원하는 결과나 데이터 수집을 찾을 확률 
  - '관측된 사건이 고정된 상태'에서 확률분포가 변화할 때의 확률 
  
  - **최대우도법 (Maximum Likelihood Estimation)**
    - 관측된 데이터들을 가장 잘 표현할 수 있는 확률분포의 매개변수를 찾는 알고리즘 

</br>

- $L(\theta | x) = P(x | \theta) = p_\theta(x) = P_\theta(X = x)$
  
  - $x$ : 관측값, $\theta$ : 모수 (Parameter), 요약통계량 
  
  - **$L(\theta | x)$** : 관측값이 주어졌을 때, 변화되는 확률 분포에서 주어진 관측값이 나올 확률
  - **$P(x | \theta)$** : 확률분포가 주어졌을 떄, 변화되는 관측값이 나올 확률 

</br>

***REF***
- [[개념정리] Likelihood와 Probability](https://xoft.tistory.com/30)
- [확률 (probability)과 가능도(likelihodd) 그리고 최대우도추정 (likelihood maximization)](https://jjangjjong.tistory.com/41)
- [Probability Model (확률 모형) 및 likelihood 개념 학습](https://gaussian37.github.io/ml-concept-probability_model/)
- [Youtube - statQuest : Maximum Likelihood](https://www.youtube.com/watch?v=XepXtl9YKwc)

</br>

[BACK TO HEAD](#Contents_of_Statistics)

---
