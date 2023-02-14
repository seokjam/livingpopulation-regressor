# livingpopulation-ml

# 안녕하세요^^ 
# AI 모델링 시간에 오신 여러분을 환영합니다.

## 오늘은 날씨, 미세먼지, 공휴일 데이터를 활용하여 서울시 <u>생활인구</u>를 예측해 보겠습니다.

<img src = "https://images.unsplash.com/photo-1528642474498-1af0c17fd8c3?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2069&q=80" width=100% align="center"/>

<div align="right">Photo by <a href="https://unsplash.com/it/@ryoji__iwata?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Ryoji Iwata</a> on <a href="https://unsplash.com/images/people?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a></div>

# Chapter1. 데이터 수집 및 분석 
> ***실습 파일 : 1. 데이터 수집 및 분석.ipynb***
### **1) 실습 순서**
- 환경 준비
- 데이터 탐색하기
- 데이터 가공하기

### **2) 실습 내용**

- 실습에 필요한 라이브러리를 불러 옵니다.
- 대상 데이터를 읽어와 탐색하며 이해합니다.
- 데이터들을 공통의 키 값으로 합칩니다.
- 실습에 필요한 컬럼만 남기고 파일로 저장합니다.

### **3) 기본 데이터**

**① 서울시 종로구의 <u>생활인구</u> 데이터**
> - **일자** : 20170101 ~ 20191231 <br>
> - **시각** : 0 ~ 23 <br>
> - **자치구코드** : 생활 인구를 측정한 자치구 코드(종로구) <br>
> - **총생활인구수** : 생활 인구 합계 <br>
> - **남0-9세, 남10-14세, 남15-19세, ... , 남65-69세   , 남70세이상** : 남성 연령별 인구 합계
> - **여0-9세, 여10-14세, 여15-19세, ... , 여65-69세   , 여70세이상** : 여성 연령별 인구 합계 <br>
    *제공정보는 통계적추정방법에 의해 추계되기 때문에 소숫점이하 정보가 존재하며,* <br>
    *정보 제공시 소수점 이하를 반올림처리함에 따라 각 속성정보의 합이 생활인구 총량과 일치하지 않을 수 있음.*

**② 서울시 <u>종관기상관측(날씨)</u> 데이터** 
> - **일자** : 20170101 ~ 20191231 <br>
> - **시각** : 0 ~ 23 <br>
> - **기온(°C)** : 대기의 온도 <br>
> - **강수량(mm)** : 어떤 시간 동안 땅에 떨어지는 비나 눈이나 우박 등을 물로 녹여서 잰 물의 깊이(두께) <br>
> - **풍속(m/s)** : 단위 시간에 공기가 이동한 거리 <br>
> - **풍향(16방위)** : 바람이 불어오는 방향 <br>
> - **습도(%)** : 공기의 건조하고 습한 정도<br>
> - **일조(hr)** : 실제로 빛이 비친 시간<br>
> - **일사(MJ/m2)** : 지표면에 도달한 태양복사에너지<br>
> - **적설(cm)** : 지면에 쌓인 눈<br>

**③ 서울시 <u>황사관측(미세먼지)</u> 데이터**
> - **일자** : 20170101 ~ 20191231 <br>
> - **시각** : 0 ~ 23 <br>
> - **1시간평균 미세먼지농도(㎍/㎥)** : 

**④ 한국천문연구원 <u>특일(공휴일)</u> 정보 데이터** 
> - **일자** : 20170101 ~ 20191231 <br>
> - **요일** : 해당 일자의 요일 <br>
> - **휴일유무** : Y, N <br> 
> - **법정공휴일명** : 법정공유일 이름 <br>

 <font color='red'>*※ 모든 데이터는 2017-2019년 데이터를 기준으로 함.<br>
2020~2022년 데이터의 경우 코로나19로 시민들은 외부 이동을 자제하고 주거지에서만 생활하는 시간이 늘어난 부분이 있어,<br>
코로나19의 영향력을 확인하는 연구가 아니라면 보통 해당 기간의 데이터들은 제외하고 통계 조사 및 연구를 진행하고 있습니다.*
</font>

---

# Chapter2. 데이터 전처리 
> ***실습 파일 : 2. 데이터 전처리.ipynb*** 
### **1) 실습 순서**
- 환경 준비
- 결측치 처리하기
- 이상치 처리하기
- 범주형 변수 가변수화하기(원-핫 인코딩)
- 데이터 정규화하기 (MinMaxScaler)

### **2) 실습 내용**

- 대상 데이터를 읽어와 탐색하며 이해합니다.
- 결측치를 확인하고 처리합니다.
- 시각화 등을 통해 이상치를 확인하고 처리합니다.
- 범주형 변수를 구분하고 Pandas 라이브러리의 get_dummies() 함수를 활용하여 가변수화를 진행합니다.

---

# Chapter3. AI 모델링 
> ***실습 파일: 3. AI 모델링.ipynb***
### **1) 실습 순서**
- 환경 준비
- Train, Test 데이터셋 분할
- 데이터 정규화 (MinMaxScaler)
- 머신러닝 모델 구현
- 머신러닝 성능 평가
- 결과 예측하기

### **2) 실습 내용**

- 대상 데이터를 읽어와 탐색하며 이해합니다.
- 데이터에서 Feature와 Target을 분리합니다.
- 데이터를 학습용 데이터와 평가용 데이터로 분리합니다.
- Feature Scaling 작업을 통해 변수들의 범위를 일정한 수준으로 조정합니다.
- 다양한 머신러닝 알고리즘을 사용해 모델링합니다.
- 성능 평가 결과를 이해하고 설명합니다.


