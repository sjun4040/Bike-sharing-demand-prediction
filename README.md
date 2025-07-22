# 🚲 자전거 대여량 예측 모델 개발 프로젝트
자전거 대여량 데이터를 이용하여 대여 수요를 예측하는 모델을 개발하는 프로젝트 입니다.
---
<p align="center">
  <img src="./Gemini_Generated_Image_s3fm7ts3fm7ts3fm.png" width="800" heigh='auto'>
</p>
대표이미지로 사용된 사진은 AI(Gemini)를 이용해서 만들었습니다

## 데이터 출처
Kaggle의 Bike Sharing Demand 데이터를 사용하였습니다.<br>
[출처] https://www.kaggle.com/c/bike-sharing-demand/data
---
## ⚙️ 분석 과정
### EDA
**주요 인사이트**<br>
  'count'는 오른쪽으로 치우친 분포를 보여 **로그변환** 필요<br>
  'hour'와 'workingday'를 보아 **주중/주말 출퇴근 패턴** 발견<br>
  'temp'와 'atemp'의 상관관계가 0.98로 **다중공선성** 문제유발 가능성 발견

### 전처리
  'datetime'열을 년,월,일,시간로 분리<Br>
  'count' 타겟 변수에 로그 변환 적용<br>
  'humidity' 이상치를 이전 시간 값으로 대체<br>
  'atemp' 열 제거 <br>
  범주형 피처 **원-핫 인코딩** 적용<Br>
  **피처 스케일링** 적용

### 모델 
Ridge Regression, RandomForest Regressor, XGBoost 모델 사용

### 모델별 학습 데이터
Ridge 회귀모델 <br>
피처의 크기(Scale)에 민감한 선형 모델의 특성을 고려하여, <br>
StandardScaler로 정규화된 데이터를 학습에 사용<br>

RandomForest 모델 <br>
피처 스케일링에 영향을 받지 않는 트리 기반 모델의 특성에 따라, <br>
원-핫 인코딩만 완료된 비정규화 데이터를 학습에 사용했습니다<br>

XGBoost 모델<br>
RandomForest와 동일하게 스케일링은 적용하지 않았으며,<br>
라이브러리 호환성 확보를 위해 열 이름의 특수 문자를 제거한 데이터를 학습에 사용했습니다<br>

### 하이퍼파라미터 튜닝
'RandomizedSearchCV'를 통해 최적 파라미터를 탐색, 최종 모델 성능 확보<br>
**결과표**<br>
| Model         | R² Score | <Br>
| Ridge         | 0.7976   | <br>
| RandomForest  | 0.8772   |  <br>
| XGBoost       | 0.9186   | <br>
----
Optimal Hyperparameters<br>
**Ridge** : alpha: 9.80    <br>
**RandomForest** : max_depth: 26<br>min_samples_leaf: 2<br>min_samples_split: 3<br>n_estimators: 319 <br>
**XGBoost** : colsample_bytree: 0.63<br>learning_rate: 0.12<br>max_depth: 3<br>n_estimators: 866<br>subsample: 0.92
## 📈 최종 모델 성능 
 **최종 모델** : **XGBoost**<br>
 **교차 검증 평균 R²** : **0.919**
----
## 사용 기술
<p align="left"> 
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
<img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" />
<img src="https://img.shields.io/badge/RandomForest-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" />
<img src="https://img.shields.io/badge/XGBoost-006B3E?style=for-the-badge&logo=python&logoColor=white" />
</p>
