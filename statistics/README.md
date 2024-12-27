# #Contents_of_Statistics
* [신뢰구간, p 값의 의미 - #1](#1)
* [중심극한정리의 의미 - #2](#2)
* [샘플링 (Sampling), 리샘플링 (Resampling)의 의미 - #3](#3)
* [가능도 (Likelihiood), 확률 (Probability)의 의미 - #4](#4)
* [고유값 (Eigen value), 고유벡터 (Eigen Vector) - #5](#5)
* [공분산 (Covariance), 상관계수 (Correlation) - #6](#6)
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

## #5
### 고유값 (Eigen value), 고유벡터 (Eigen Vector)

- **고유벡터 (Eigen Vector)**
  - 선형 변환이 일어난 후에도 방향이 변하지 않는 0이 아닌 벡터

- **고유값 (Eigen value)**
  - 고유벡터의 길이가 변하는 고유벡터에 대응하는 값

- **고유공간 (Eigen Space)**
  - 고유값 $\lambda$의 고유공간은 그 고유벡터들과 0으로 구성되는 부분 벡터 공간 
  - 고유공간 $V_{\lambda} = \{v \in V: Tv = \lambda v\}$

- **고유기저 (Eigen Basis)** 
  - 선형 변환 $T$의 고유벡터들로 구성된 $V$의 기저
    - 기저 : 벡터공간 $V$을 선형 생성하는 선형 독립을 만족하는 벡터들 

</br>

### ***  벡터 공간 $V$ 위의 선형 변환 $T : V \rightarrow V$가 주어졌을 때, 
- 어떤 $v \in V$, $\lambda \in K$가 $v \neq 0$, $Tv = \lambda v$를 만족한다면 
  - => $v$를 $T$의 '**고유벡터**'
  - => $\lambda$를 $T$에 대응하는 '**고유값**'

</br>

- **성질** 
  - 선형 변환 $T : V \rightarrow V$ 에 대해 
    - $\lambda$ 가 $T$의 고유값
    - $\lambda I - T$가 특이 행렬
      - 특이 행렬 : 역행렬을 가지지 않는 행렬
    - $det(\lambda I - T) = 0$, 즉 $\lambda$가 고유 다항식의 근을 만족한다.

- **활용 및 중요성**
  - **주성분 분석 (PCA)**
    - 데이터를 압축하는데 사용되는 일반적인 차원 축소 기술 
      - '고유벡터' = 주성분 벡터 : 분산이 큰 방향
      - '고유값' : 대응하는 분산의 크기 
    - 활용 
      - 차원 축소를 통한 시각화 및 기하학적 해석
      - PCA를 통한 변수추출을 통한 선형 회귀에서의 다중공선성 문제 완화
  
  - **특이값 분해 (SVD)**
    - 대각화를 통한 행렬 분해
    - 활용
      - 데이터 분해 및 근사를 통한 데이터 압축, 노이즈 제거등 활용
  
  #### => 주성분 분석 (PCA), 특이값 분해 (SVD) 정리 필요

</br>

***REF***
- [고윳값과 고유 벡터](https://ko.wikipedia.org/wiki/%EA%B3%A0%EC%9C%B3%EA%B0%92%EA%B3%BC_%EA%B3%A0%EC%9C%A0_%EB%B2%A1%ED%84%B0)
- [고유값(eigen value)과 고유벡터(eigen vector)](https://gguguk.github.io/posts/eigenvalue_eigenvector/)
- [[선형대수학 #3] 고유값과 고유벡터 (eigenvalue & eigenvector)](https://darkpgmr.tistory.com/105)
- [머신러닝에서 고유값의 활용](https://brunch.co.kr/@chris-song/104)
  
</br>

[BACK TO HEAD](#Contents_of_Statistics)

---

## #6
### **공분산 (Covariance, Cov)**
  * $Cov(X, Y) = E[(X-E[X])(Y-E[Y])]$
  * $E(X) = \mu, \, E(Y) = v$ 일 때,  $Cov(X, Y) = E(X \cdot Y) - \mu v$

  </br>

  * **2개의 확률변수의 선형 관계 및 관련성**를 나타내는 값 
    * 한 확률변수의 값이 상승하는 경향을 보일 때  
      * 다른 확률변수의 값이 상승하는 경향을 보인다면 => '양'의 공분산 값
      * 다른 확률변수의 값이 하강하는 경향을 보인다면 => '음'의 공분산 값
  
  * 측정 단위의 크기에 따라 값이 달라짐 
    * $Cov(X, Y)$의 단위 = $X$, $Y$의 곱

  * 표본 공분산 (피어슨 상관계수에 사용)
    * $Cov(X, Y)$ $=$ $\sum_{i}^{n}(X_i - \bar X)(Y_i - \bar Y)$ $/ ({n-1})$

  * **성질**    
    * $Cov(X, X) = Var(X)$
  
    * $Cov(X, Y) = Cov(Y, X)$
  
    * $Cov(aX, bY) = ab Cov(X, Y)$
  
    * $Cov(\sum_{i=1}^{n}X_i, \sum_{j=1}^{n}Y_j) = \sum_{i=1}^{n}\sum_{j=1}^{n}Cov(X_i, Y_j)$

    * $Var(X \pm Y) = Var(X) + Var(Y) \pm 2 Cov(X, Y)$
  
    * $Var(\sum_{i=1}^{n}X_i) = \sum_{i=1}^{n}Var(X_i) + 2 \sum_{i, j \, : \, i < j}Cov(X_i, X_j)$
  
    * 두 확률변수 $X$, $Y$가 독립일 때, $Cov(X, Y) = 0$을 만족
      * 두 확률변수 $X$, $Y$가 독립 => $E(X \cdot Y) = E(X)E(Y) = \mu v$
      * $Cov(X, Y) = E(X \cdot Y) - \mu v =  \mu v -  \mu v = 0$ 

</br>

### 상관계수 (Correlation, Corr)
  * **피어슨 상관계수**$\,$ $r_{XY} = \frac{\sum_{i=1}^{n}(X_i - \bar X)(Y_i - \bar Y)} {\sqrt{\sum_{i=1}^{n}(X_i - \bar X)^2} \sqrt{\sum_{i=1}^{n}(Y_i - \bar Y)^2} } = \frac{Cov(X, Y)}{\sigma_X \sigma_Y}$
    * '연속형' 데이터에 적합
  
  * **스피어만 상관계수**$\,$ $\rho = \frac{\sum_{i=1}^{n}(x_i - \bar x)(y_i - \bar y)} {\sqrt{\sum_{i=1}^{n}(x_i - \bar x)^2} \sqrt{\sum_{i=1}^{n}(y_i - \bar y)^2} }$
    * $x_i$ = X에서의 i번째 데이터 순위, $y_i$ = Y에서의 i번째 데이터 순위 
    *  $d_i = x_i - y_i$ 일 때, $\rho = 1 - \frac{6 \sum d_i^2}{n(n^2 - 1)}$
    *  '이산형', '순서형' 데이터에 적합

  </br>

  * **두 변수 사이의 통계적 관계를 표현**하기 위해 특정한 상관 관계의 정도를 수치적으로 나타낸 계수
  
  * 값의 범위가 -1, +1 사이에 속함 
    * $\pm 1$은 가장 센 잠재적 일치, 0은 가장 센 잠재적 불일치를 나타냄

</br>

### 공분산 vs 상관계수
  * 공분산 
    * 두 확률변수 $X$, $Y$의 측정 단위와 범위에 영향을 받음 
      * 두 확률변수 $X$, $Y$의 관계의 방향만 알 수 있음
  
    * 두 확률변수 $X$, $Y$가 독립일 때, $Cov(X, Y) = 0$을 만족
  
    * $Cov(X, Y) = 0$ 일 때, 두 확률변수 $X$, $Y$가 독립이 아닐 수 있음

  * 상관계수 
    * 공분산을 표준화시켜 객관성을 확보, 단위를 갖지 않음
  
    * 상관관계가 존재한다고 인과관계가 존재하지 않음
  
    * 인과관계가 존재한다면 상관계수가 존재함

</br>

***REF***
- [위키백과 - 공분산](https://ko.wikipedia.org/wiki/%EA%B3%B5%EB%B6%84%EC%82%B0)
- [위키백과 - 상관계수](https://ko.wikipedia.org/wiki/%EC%83%81%EA%B4%80%EA%B3%84%EC%88%98)
- [위키독스 - 공분산, 상관계수](https://wikidocs.net/202424)

</br>

[BACK TO HEAD](#Contents_of_Statistics)

---