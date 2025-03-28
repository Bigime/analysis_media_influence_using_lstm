# Analysis-of-media-influence-using-LSTM-model

## 개요
### 언론의 영향력 확인을 위해 LSTM을 이용한 전세가격예측모델을 만들었습니다.
### 전세가격과 관련된 뉴스를 추출 후 뉴스로부터 감성수치를 산출한 뒤 감성수치를 넣었을 때 넣지 않았을 때의 예측 성능의 차이를 비교하여 언론의 영향력이 있는지를 검증하고자 했습니다.
---

## 분석 단계

## 뉴스 
<img src="https://github.com/user-attachments/assets/f29a0845-d5b6-40bd-acbb-fa85f7f55da8"  width="600" height="400"/>


### 1. 전세가격과 관련된 기사만 뽑고자 하여 LDA를 도입했습니다.
### 2. 각 기사마다 토픽의 비중을 산출하고 토픽들 중 전세가격과 관련된 토픽의 비중을 가중치로 부여하여 해당 기사에 대한 감성수치를 산출했습니다.
### 3. 전세가격과 관련된 토픽을 뽑기 위해 기사마다 토픽별 비중 * 감성수치로 토픽별 감성수치를 만든 뒤 상관관계 행렬을 만들고 토픽모델링 결과 산출된 토픽별 단어들을 활용해 토픽을 추렸습니다.
<img src="https://github.com/user-attachments/assets/c2b15711-1b46-4571-aa5a-fea626d45210"  width="600" height="400"/>

## 감성수치를 넣은 LSTM 모델과 감성수치를 넣지 않은 LSTM 모델의 비교

<img src="https://github.com/user-attachments/assets/ba52bfe4-5867-4117-a3e1-222afde85b5f"  width="600" height="400"/>


### 1. sequence_length를 동일하게 하고 time_seris_split을 통해 훈련데이터와 테스트데이터로 분할했습니다.

<img src="https://github.com/user-attachments/assets/0ce2da62-1437-4a2c-8fc9-0a2fcff71cfb"  width="600" height="400"/>

### 2. 전체 예측성능에 있어서 차이가 없었습니다.
#### 감성수치 포함한 모델 : 0.145 vs. 감성수치 포함하지 않은 모델 : 0.135

### 3. 하지만 구간을 나눠본 결과 fold1에서 예측성능의 차이가 크게 났습니다.
<img src="https://github.com/user-attachments/assets/dfc0944a-93bc-4e93-9a3d-4449d79c6dcd"  width="600" height="400"/>

### 4. fold1에 대해서 사후분석한 결과 학습량 부족으로 인해 감성수치를 추가한 것이 예측 성능에 악영향을 끼쳤습니다.
<img src="https://github.com/user-attachments/assets/4cd2f449-11e9-41dd-aafa-469ed872d3fb"  width="600" height="400"/>

---

## 보완할 점

### 1. 토픽별 감성수치간의 상관성을 상관관계 행렬 이외에 다른 방법을 이용해볼 수 있습니다.
### 2. 전세가격지수를 실제 활용할 때는 범주형 범수로 사용하기 때문에 regression 보다는 classification모델을 사용하여 전세가격지수에 대한 예측을 진행하는 것이 맞다고 판단했습니다.
### 3. LDA를 활용해 기사의 토픽을 추출할 때 토픽모델링의 불완전성으로 인해 일부를 제외하고 시간에 따른 경향성이 비슷하게 나타났습니다.
