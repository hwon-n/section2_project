# 프로젝트 제목

## 💻 프로젝트 소개

[Kaggle에서 제공되는 데이터](https://www.kaggle.com/datasets/subhamjain/loan-prediction-based-on-customer-behavior?select=Training+Data.csv)를 기반으로 채무 불이행 여부에 대해 예측을 하는 머신러닝 모델을 만들어본 프로젝트입니다. 

<br />


## 🎮 개발 기간

21.11.08 - 21.11.11

<br />

## 🛠 사용 툴

* Colab
* Python
  * pandas
  * sklearn
  * eli5
  * shap

<br />

## 사용 데이터

|컬럼명|컬럼 설명|
|----|----|
|ID|아이디|
|Income|소득|
|Age|나이|
|Experience|경력(year)|
|Married/Single|결혼 여부|
|House_Ownership|집 소유 여부|
|Car_Ownership|차 소유 여부|
|Profession|직업|
|CITY|거주 지역|
|STATE|거주 지역|
|CURRENT_JOB_YRS|현재 직장 근무 년수|
|CUREENT_HOUSE_YRS|현재 집 거주 기간|
|Risk_Flag|대출 채무 불이행 여부|

<br />

  
## 🔎 주요 내용

### 데이터 전처리

|컬럼명|변경 내용|
|----|----|
|ID|필요 없는 컬럼이라 판단되어 삭제해줌|
|Age|30대 미만, 30대, 4-50대, 60대 이상 총 4가지 그룹으로 나눠줌|
|Experience|년수에 따라 Entry, Intermediate, Mid, Senior 4가지 그룹으로 나눠줌|
|CITY|범주가 너무 많아 학습에 오히려 방해가 될 것 같아 삭제해줌|
|STATE|북부 지역과 아닌 지역으로 나눠줌|
|CURRENT_JOB_YRS|5년 미만은 1로, 10년 이하는 2로, 10년을 넘긴 경우 3으로 나눠줌|


<br />

### 모델 학습

기존에 배웠던 모델을 활용해보고자 `Logistic Regression`과 `Decision Tree`, `RandomForest` 세 모델과 개인적으로 관심을 갖고 있던 모델인 `XGBClassifier`를 간단하게 구현해 학습시켰습니다. 그 중에서 제일 성능이 좋게 나온 **RandomForest** 모델을 최종적으로 선택했습니다. 

그리고 하이퍼파라미터 튜닝을 수동으로 진행해서 간단하게 구현한 모델 말고 새로운 모델을 구현해서 성능 테스트를 진행해봤습니다. 그 validation dataset의 정확도는 0.8579, test dataset의 정확도는 0.8568이 나왔습니다. 

<br />


### 시각화

**permuter & eli5**

![image](https://user-images.githubusercontent.com/52039588/217028278-f330c375-90ec-46b5-a3e5-4bff4162ee77.png)

permuter를 활용해 feature importances를 확인한 후 eli5를 사용해서 보기 좋게 시각화를 진행해봤습니다.

<br />

**Shap force_plot**

![image](https://user-images.githubusercontent.com/52039588/217028496-e4736edf-d91a-4286-889a-211e1625c020.png)

특정 데이터를 해석하기 위해 Shap의 force_plot을 활용해봤습니다. 예측값에 긍정적인 요인은 준 컬럼은 빨간색으로, 부정적인 요인은 파란색으로 표현이 됐습니다. 또한 크기를 크게 차지한 컬럼일수록 크게 영향을 끼친 컬럼입니다. 

<br />

**Shap waterfall_plot**

![image](https://user-images.githubusercontent.com/52039588/217029365-00b0337b-0faf-4e8c-a89c-df7d84e647a7.png)

특정 데이터가 예측된 근거를 보여주는 plot입니다. 각 컬럼들의 공헌도와 shapley value를 직관적으로 표현하는게 특징인 그래프입니다. 위의 force_plot과 마찬가지로 긍정적인 요인은 빨간색, 부정적인 요인은 파란색으로 표현이 됐습니다. 


<br />

**Shap summary_plot (300개)**

![image](https://user-images.githubusercontent.com/52039588/217028811-79130ede-856a-4b72-b15d-278b833756c6.png)

전체 데이터 해석할 때 사용할 수 있는 summary_plot입니다. 각 열에 대한 shapley value를 누적해 시각화해줍니다. 

저는 300개의 데이터만 사용했고, 위의 사진에서는 19번째, 131번째, 235번째 데이터에 어떤 컬럼이 긍정적이고 부정적인 영향을 끼쳤는지 한눈에 확인할 수 있습니다. 



<br />
