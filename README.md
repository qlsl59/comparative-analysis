# 농산물 가격 예측 모델 개발 및 상위 팀 비교 분석

## 프로젝트 정보

- **사용 언어**: Python
- **개발 환경**: VSCODE, Google Colab
- **인원**: 3명 (임하은, 박성빈, 원현아)
- **기간**: 2024.10.01 ~ 12.08

## 주요 내용

### 프로젝트 개요
- **공모전**: DACON 데이터, AI를 활용한 물가 예측 경진대회 (농산물 가격 중심)
- **목표**: 농산물 가격 예측을 통해 물가 안정성 및 시장 동향 반영
- **분석 대상**: 배추, 무, 양파, 사과, 배, 건고추, 깐마늘, 감자, 대파, 상추 등 10개 농산물

### 분석 데이터
- **데이터 출처**: DACON 제공 데이터
- **데이터 구성**:
  - **Train Data**: 2018년 ~ 2021년의 순단위(10일) 데이터
  - **Test Data**: 2022년의 순단위 데이터 (추론 시점 T 비식별화)
- **평가 방식**: 추론 시점 T 기준으로 최대 3개월의 순단위 입력 데이터를 바탕으로 T+1순, T+2순, T+3순의 평균가격 예측

### 데이터 전처리
- **데이터 병합**: 전국도매시장 데이터와 산지공판장 데이터 병합
- **품목 선정**: 사용 가능한 품목 선정 및 시각화를 통해 변화 분석
- **시점 변환 및 정규화**: LSTM 모델에 적합한 형태로 데이터 준비
- **데이터 그룹화**: 시점, 품목명, 품종명, 거래단위, 등급을 기준으로 그룹화 및 평균가격 계산

### 모델링
- **사용 모델**: LSTM (Long Short-Term Memory)
  - **학습 설정**: epochs 200, batch_size 32
  - **예측**: test_data에 적용하여 예측 수행
  - **결과 복원**: 정규화된 값을 원래 스케일로 복원 및 그룹 평균 계산
- **시계열 데이터셋 생성**: 슬라이딩 윈도우 기법을 사용하여 과거 데이터 기반 미래 예측 데이터셋 준비

### 모델링 결과
- **시간별 승차량 차이**: train data와 test data 비교
- **요일별 승차량 차이**: train data와 test data 비교

## 공모전 수상작 분석

### 팀 <나서스>
- **데이터 활용**: 외부 meta 데이터와 결합하여 데이터 중강
- **전처리**: Sliding Window 기법으로 데이터 재구조화, Sin/Cos 변환으로 계절성 반영
- **모델링**: 품목별 특성에 따라 XGBoost, Extra Trees, RANSAC 모델 선택
- **계절성 반영**: Sin/Cos 변환 및 피크/바닥 분석을 통해 계절적 패턴 학습

### 팀 <푸롯푸롯>
- **데이터 활용**: 수출입 데이터를 활용해 신선식품의 순수입량 계산
- **전처리**: 날씨 데이터를 순 단위로 변환, 통계적 변수 생성
- **모델링**: Tree 기반 모델 (Random Forest, XGBoost, AutoGluon) 사용
- **계절성 반영**: Mann-Kendall Test를 통해 계절적 트렌드 분석

## 프로젝트와 수상작 비교 분석

### 데이터 활용
- **우리 팀**: 주어진 데이터만 사용, 데이터 중강 시도하지 않음
- **수상 팀**: 외부 데이터 통합 및 데이터 중강을 통해 시장 특성 반영

### 전처리 및 피처 엔지니어링
- **우리 팀**: 단순 스케일링 적용, 추가적인 피처 생성 부족
- **수상 팀**: Sliding Window 기법, Sin/Cos 변환 등 복잡한 패턴 학습 가능한 구조화

### 모델링
- **우리 팀**: 단일 LSTM 모델 사용
- **수상 팀**: 품목별 특성에 맞는 다양한 모델 선택 및 최적화

### 계절성 반영
- **우리 팀**: 계절성 고려하지 않음
- **수상 팀**: 계절성 데이터 정량화 및 파생 변수 활용

## 결론 및 학습점

### 프로젝트 결론
- 데이터 활용: 제공된 데이터만 사용하여 한계점 존재
- 전처리: 단순 스케일링에 그쳐 복잡한 패턴 학습 부족
- 모델링: 단일 모델 사용으로 품목별 특성 반영 어려움
- 계절성: 계절성 데이터를 고려하지 않아 모델이 해당 패턴 학습하지 못함

### 학습점
- 데이터 활용의 중요성: 데이터 중강 및 통합을 통해 더 깊이 있는 분석 가능
- 전처리 및 피처 엔지니어링: 데이터의 본질적 특성을 드러낼 수 있는 통계적 분석 및 파생 변수 생성 필요
- 다양한 모델의 필요성: 단일 모델이 아닌 데이터 특성에 맞는 모델 선택 및 하이브리드 접근 방식 고려
- 계절성 반영: 계절적 패턴이 강한 데이터를 다룰 때, 이를 정량화하고 모델이 학습할 수 있도록 설계 필요

## 프로젝트 조직 (역할 분담)

- **박성빈 (팀장)**: 프로젝트 총괄
- **임하은**: 데이터 분석 및 모델링, 발표 자료 제작
- **원현아**: 데이터 전처리 및 시각화, 발표

---

**가늠 팀**  
임하은, 박성빈, 원현아
