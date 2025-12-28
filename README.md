# Item-based Collaborative Filtering Project using MovieLens Dataset

MovieLens 데이터셋을 활용한 Item-based Collaborative Filtering 추천 시스템 프로젝트입니다.

## 📋 프로젝트 개요

본 프로젝트는 협업 필터링(Collaborative Filtering) 기반의 영화 추천 시스템을 구현하고, 다양한 기법을 적용하여 성능을 개선하는 과정을 담고 있습니다.

## 🎯 주요 내용

### 1. 데이터 탐색적 분석 (EDA)
- 평점 분포 및 사용자/아이템 활동 희소성 분석
- 장르 인기 및 분포 분석
- 시간 흐름에 따른 평점 변화 추이
- 태그 사용 현황 분석
- 장르 간 상관관계 분석
- 사용자별 평점 성향 분석

### 2. 코드 개선 과정

#### 코드 1: Mean Centering (평균 중심화)
- 사용자의 평균 평점을 기준으로 정규화
- 가장 기본적인 정규화 방법

#### 코드 2: Z-Score + Dot Product
- Z-Score 정규화 적용으로 사용자별 평점 성향 차이 보정
- Dot Product를 활용한 유사도 계산
- K=20 이웃 사용

#### 코드 3: K 이웃 제한 제거
- 양수 유사도를 가진 모든 아이템 사용
- 데이터 희소성 문제 대응

#### 코드 4: Fallback 방식 + 행렬 계산 최적화
- 예측 불가능한 경우를 위한 Fallback 로직 추가
- NumPy 행렬 연산으로 계산 속도 개선
- **기준 성능**: RMSE 0.8573 ± 0.0144, MAE 0.6522 ± 0.0104

#### 코드 5: IUF (Inverse User Frequency) 적용
- 사용자 빈도 역수를 활용한 가중치 적용

#### 코드 6: IMDB 데이터 활용 하이브리드 모델
- 평점 유사도 + 배우 유사도 + 감독 유사도 통합
- **성능**: RMSE 0.8488 (baseline 0.8534 대비 개선)

### 3. 하이브리드 모델

#### 평점 + 장르 유사도 모델
- HYBRID_ALPHA = 0.9 (평점 90%, 장르 10%)
- 평균 RMSE: 0.8588

#### 평점 + 태그 유사도 모델
- 최적 가중치: 평점 20% + 태그 80%
- 그리드 서치를 통한 최적 파라미터 탐색

#### 평점 + 장르 + 태그 유사도 모델
- 최적 가중치 조합 (그리드 서치):
  - W_RATING: 0.20
  - W_GENRE: 0.00
  - W_TAG: 0.80
  - 평균 RMSE: 0.8608
- 베이지안 최적화를 활용한 효율적인 파라미터 탐색

### 4. 최적화 기법

- **Significant Weighting**: 유사도 계산 시 공통 평가 수를 고려한 가중치 적용
- **Grid Search**: 체계적인 파라미터 탐색
- **Bayesian Optimization**: 이전 평가 결과를 학습하여 효율적인 최적화

## 📁 프로젝트 구조

```
BigDataAlgorithm/
├── 1.original_baseline_code(remove_K_ver)/     # 원본 베이스라인 코드
├── 1_1.revise_baseline_code(effi_up)/          # 효율성 개선 코드
├── 2.add_genres_similarity_vector/              # 장르 유사도 벡터 추가
├── 3.Significance Weighting/                    # Significant Weighting 적용
├── 4.add_tagData_vector/                        # 태그 데이터 벡터 추가
├── 5.rating+tag+geners/                         # 평점+태그+장르 하이브리드 모델
├── 최종 3조.ipynb                                # 전체 실험 결과 통합 노트북
└── data/                                        # MovieLens 데이터셋
    ├── ratings.csv
    ├── movies.csv
    ├── tags.csv
    └── links.csv
```

## 🔧 사용 기술

- **Python**: 주요 프로그래밍 언어
- **Pandas**: 데이터 처리 및 분석
- **NumPy**: 수치 연산 및 행렬 계산
- **Scikit-learn**: 코사인 유사도 계산, 베이지안 최적화
- **Matplotlib/Seaborn**: 데이터 시각화

## 📊 주요 성과

- Baseline 대비 RMSE 개선 (0.8534 → 0.8488)
- 행렬 연산 최적화로 계산 속도 향상
- 하이브리드 모델을 통한 추천 정확도 개선
- 베이지안 최적화를 활용한 효율적인 하이퍼파라미터 탐색

## 📝 참고

- 데이터셋: [MovieLens Dataset](https://grouplens.org/datasets/movielens/)
- 각 폴더의 노트북 파일에서 상세한 실험 과정과 결과를 확인할 수 있습니다.

