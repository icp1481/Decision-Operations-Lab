# KAIST Decision & Operations Lab Research Project

**지도교수:** 민승기 교수님  
**Lab 링크:** [KAIST Decision & Operations Lab](http://do.kaist.ac.kr/)  

---

## I. 연구 주제

**Delayed Feedback과 Batched Decision-Making 환경에서 Multi-Armed Bandit (MAB) 알고리즘을 활용한 자원 배분 최적화**

---

## II. 연구 문제 세팅

### 1. TalkingData AdTracking Fraud Detection Challenge 대회 소개
- **목표:** 모바일 앱 광고에서 발생하는 부정 클릭(클릭 사기, fraud)을 식별하는 Kaggle 대회
- **데이터셋:** IP 주소, 앱, 디바이스, 운영 체제, 채널 등 클릭과 관련된 다양한 피쳐 제공
- **과제:** 주어진 데이터를 활용하여 머신러닝 모델을 개발, 클릭이 부정 클릭인지 예측
- **평가 기준:** ROC-AUC

### 2. 연구 시스템 설계
- **문제 인식:** 모든 클릭에 대해 fraud 검사를 진행하면 검사 비용이 많이 들고, 검사 정확도 또한 낮음
- **목적:** 매 시간마다 클릭들을 그룹으로 분리하여, 각 그룹에 할당할 fraud 검사의 양을 최적화
- **알고리즘 제안:** 
  - 기본 알고리즘: 각 그룹에 uniform하게 검사를 할당
  - 개선 알고리즘: Multi-Armed Bandit (MAB)와 Gittin Index를 활용하여 검사 할당 최적화

---

## III. 연구 진행

### 1. 데이터 분석 및 머신러닝 모델 개발
- **EDA (Exploratory Data Analysis):**  
  - 약 24시간 주기의 클릭 분포 확인
- **데이터 전처리 및 그룹 구분:**  
  - PCA를 활용한 데이터 압축 및 그룹 구분
- **모델 개발:**  
  - 사용 모델: XGBoost, LightGBM  
  - **결과:** XGBoost 모델이 더 우수한 성능을 보임  
  - **피쳐 분석:** app 변수 위주의 LDA(Latent Dirichlet Allocation) 피쳐가 큰 기여

### 2. Fraud Detection 알고리즘 개발
- 머신러닝 모델이 예측한 fraud 확률을 기반으로 각 클릭의 fraud 여부 결정
- **검사 할당 방식 비교:**  
  - **Uniform 방식:** 각 그룹에 균등하게 검사 할당  
  - **MAB 기반 알고리즘:** 그룹별 검사 할당을 최적화하여 보다 효율적인 fraud 검출 도모

### 3. 참고 논문
- Bastani, H., Drakopoulos, K., Gupta, V., Vlachogiannis, I., Hadjichristodoulou, C., Lagiou, P., Magiorkinis, G., Paraskevis, D., & Tsiodras, S. (2021). *Efficient and targeted border testing via reinforcement learning.* Nature, 599(7884), 108–113.  
  [DOI 링크](https://doi.org/10.1038/s41586-021-04014-z)

### 4. 핵심 알고리즘 의사 코드
> ![](https://github.com/icp1481/Decision-Operations-Lab/blob/main/images/%ED%95%B5%EC%8B%AC%20%EC%9D%98%EC%82%AC%EC%BD%94%EB%93%9C.png)
---

## IV. 연구 결과

### 1. 머신러닝 모델 성능
- **ROC AUC Score:** 0.96553

### 2. Fraud Detection 성능 비교
| 할당 방식  | Fraud 검출 비율 | Total Point      |
|------------|-----------------|------------------|
| **Original**   | 57~60%          | 1,306,343        |
| **Uniform**    | 37~38%          | 873,456          |
| **Upgrade (MAB 적용)** | 61~62%          | 1,309,684        |

- **성과:** MAB 알고리즘은 uniform 방식 대비 약 1.67배 우수한 성능을 보임

### 3. Confusion Matrix
> ![](https://github.com/icp1481/Decision-Operations-Lab/blob/main/images/%EC%97%B0%EA%B5%AC%EA%B2%B0%EA%B3%BC%20-%20confusion%20matrix.png)

| Metric    | Value   |
|-----------|---------|
| Accuracy  | 0.5497  |
| Recall    | 0.6378  |
| Precision | 0.0683  |
| F1 Score  | 0.1235  |

### 4. 추가 연구 및 개선
- Prior widening C 상수 조정
- Discount factor (γ) 파라미터 최적화
- 기타 알고리즘 개선 연구 진행 중

---
