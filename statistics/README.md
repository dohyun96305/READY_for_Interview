
# Contents of Statistics
* [신뢰구간, p 값의 의미 - #1](#1)
* [중심극한정리의 의미 - #2](#2)
  
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
---

## #2
### 중심극한정리 (Central Limit Theorem)
- 동일한 확률분포를 가진 **'독립' 확률 변수 n개의 평균의 분포**는 n이 적당히 크다면 정규분포에 가까워진다는 정리
  - 일반적으로 표본의 크기가 30 이상일 때, 중심극한정리가 적용된다고 할 수 있음
  
  
- $[X_1, \ldots, X_n]$ 을 평균 $\mu$, 분산 $\sigma^2$인 분포에서 추출한 확률표본의 집합이라고 할 때, 
  
  $$E(\bar{X_n}) = E(\frac{1}{n}(X_1 + \ldots + X_n)) = \frac{1}{n}(E(X_1) + \ldots + E(X_n)) = \frac{1}{n} * (n * \mu) = \mu$$

  $$Var(\bar{X_n}) = Var(\frac{1}{n}(X_1 + \ldots + X_n)) = \frac{1}{n^2}(Var(X_1) + \ldots + Var(X_n)) = \frac{1}{n^2} * (n*\sigma^2) = \frac{\sigma^2}{n}$$

  $$Y = \frac{\sqrt{n}(\bar{X} - \mu) }{\sigma} = \frac {\sum (X_i - n \mu) }{\sigma\sqrt{n}} \sim N(0, 1)$$ 

  
- 모집단 $X_j$에 대해 추가적인 정보 없이 평균 $\mu$와 분산 $\sigma^2$만 정의된다면 </br> 
  => 중심극한정리를 통해 **표본평균의 분포가 평균 $\mu$ 와 분산 $(\frac{\sigma}{\sqrt{n}})^2$인 정규분포에 근사한다**는 것을 알 수 있음 </br>
  => **표본 통계량을 통해 모수를 추정**할 수 있는 수학적 근거를 제시함

<br>

***REF***
- [중심 극한 정리](https://ko.wikipedia.org/wiki/%EC%A4%91%EC%8B%AC_%EA%B7%B9%ED%95%9C_%EC%A0%95%EB%A6%AC)
- [중심극한정리와 정규성검증](https://speedspeed.tistory.com/202#google_vignette)
- [수리통계 - 중심극한정리](https://www.goteodata.kr/77)
- [중심 극한 정리(CLT)](https://gguguk.github.io/posts/CLT/)
--- 

