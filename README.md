# 🚲 자전거 대여량 예측 모델 개발 프로젝트
자전거 대여량 데이터를 이용하여 대여 수요를 예측하는 모델을 개발하는 프로젝트 입니다.
---
## 데이터 출처
Kaggle의 Bike Sharing Demand 데이터를 사용하였습니다.
[출처] https://www.kaggle.com/c/bike-sharing-demand/data
---
## ⚙️ 분석 과정
### EDA
**주요 인사이트**
  'count'는 오른쪽으로 치우친 분포를 보여 **로그변환** 필요
  'hour'와 'workingday'를 보아 **주중/주말 출퇴근 패턴** 발견
  'temp'와 'atemp'의 상관관계가 0.98로 **다중공선성** 문제유발 가능성 발견

### 전처리
  'datetime'열을 년,월,일,시간로 분리
  'count' 타겟 변수에 로그 변환 적용
  'humidity' 이상치를 이전 시간 값으로 대체
  'atemp' 열 제거 
  범주형 피처 **원-핫 인코딩** 적용
  **피처 스케일링** 적용

### 모델 
Ridge Regression, RandomForest Regressor 모델 사용

