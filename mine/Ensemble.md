# Voting
- 여러 모델들(다른 유형의 알고리즘 기반)의 예측 결과를 투표를 통해 최종 예측 결과를 결정하는 방법
![](https://i.imgur.com/VinYlyK.png)

## hard voting, soft voting
- hard voting: 다수 모델이 예측한 값이 최종 결과 값
- soft voting: 모든 모델이 예측한 레이블 값의 결정 확률 평균을 구한 뒤 가장 확률이 높은 값을 최종 선택
![](https://i.imgur.com/FQeU83i.png)
- 일반적으로 soft voting을 더 많이 사용
# Bagging(Bootstrap Aggregating)

- 데이터로부터 부트스트랩 한 데이터로 모델들을 학습시킨 후, 모델들의 예측 결과를 집계해 최종 결과를 얻는다.
- 같은 유형의 알고리즘 기반 모델들을 사용
- 범주형 데이터(Categorical Data)는 투표 방식(Voting)으로 결과를 집계
- 연속형 데이터(Continuous Data)는 평균으로 결과를 집게
![](https://i.imgur.com/HOvy4st.png)

## Boostrap
- 복원 램덤 샘플링 방식으로 데이터를 분할.
- 학습 데이터가 충분하지 않더라도 충분한 학습 효과를 주어 높은 bias의 underfitting 문제나, 높은 variance로 인한 overfitting 문제를 해결하는데 도움을 준다.

## Random Forest
- Bagging의 대표적인 알고리즘
- Decition Tree 알고리즘 사용
![](https://i.imgur.com/DlIFGUW.png)
![](https://i.imgur.com/JsBkzou.png)
### 주요 하이퍼파라미터
#### n_estimators
- 만들어질 Decision Tree 개수 지정(기본 값: 100)
- 많이지정할수록성능이좋아질것으로기대할수있지만무조건그런것은아님
- 너무 늘리면 학습 속도가 너무 느려질 수 있음을 고려해야 함
#### max_depth
- 트리의 최대 깊이(기본 값: None)
- 기본 값으로 설정하면 완벽히 분류될 때 까지 분할하거나, 노드가갖는샘플개수가min_samples_split 설정 값 보다 작아질 때 까지 계속 분할
#### min_samples_split
- 노드를 분할하기 위한 최소한의 샘플 개수(기본 값: 2)
- 값을 작게 설정할 수록 계속 분할 되어 트리 깊이가 깊어져 과적합 발생 가능
#### min_samples_leaf
- 리프 노드가 되기 위한 최소한의 샘플 수(기본 값: 1)
- min_samples_split과 함께 과적합을 방지할 목적으로 사용
#### max_feature
- 최선의 분할을 위해 고려할 Feature 수(기본 값:auto)
- 기본 값으로 설정하면 모든Feature를 사용해서 분할 수행
- 정수로 선언하면 Feature 수, 실수로 선언하면 Feature 비율
- 'sqrt'로 선언하면 전체 Feature 수의 루트 값
- 'auto'로 선언하면 'sqrt'와 같은 의미
- 'log'로 선언하면 log2(전체 Feature 수)
# Boosting
- 잔차를 이용하여 이전 모형의 약점을 보완
- 같은 유형의 알고리즘 기반 모델 여러 개에 대해 순차적으로 학습 수행
- 이전 모델이 제대로 예측하지 못한 데이터에 대해서 가중치를 부여하여 다음 모델이 학습과 예측을 진행하는 방법
- 배깅에 비해 성능이 좋지만, 속도가 느리고 과적합 발생 가능성 있음
- 대표 부스팅 알고리즘 : XGBoost, LightGBM
![](https://i.imgur.com/9fna0ry.png)

## XGBoost(eXtreme Gradient Boosting)
- Gradient Boosting의 순차적 학습으로 인해 오래 걸리던 시간을 병렬 학습을 가능하게 하여 극복하고자 한 알고리즘
- 

# Stacking
