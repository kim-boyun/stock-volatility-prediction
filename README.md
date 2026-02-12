# 주식 시장 변동성 예측 (ML 파이프라인 실습)

주식·VIX 데이터를 활용해 **변동성 급증 여부를 분류**하는 머신러닝 파이프라인 프로젝트입니다.  
데이터 수집 → 전처리 → 모델 학습·평가 → 시각화·보고서까지 한 번에 경험할 수 있도록 구성한 **학습/실습용** 프로젝트입니다.

---

## 사용 기술 (Tech Stack)

| 구분 | 기술 |
|------|------|
| **언어** | Python 3.8+ |
| **ML/분석** | scikit-learn, pandas, numpy |
| **데이터** | yfinance (주가·VIX), 합성 데이터(실습용) |
| **시각화** | Streamlit, Plotly |
| **보고서** | ReportLab, matplotlib |
| **테스트** | pytest |
| **기타** | joblib (모델 저장) |

> ※ 실습 편의를 위해 실제 API 대신 **합성 데이터**를 사용할 수 있는 옵션이 포함되어 있습니다.

---

## 주요 기능

- 주식 심볼·기간 설정에 따른 데이터 로드 및 변동성·기술적 지표 계산
- **다양한 분류 모델**: 로지스틱 회귀, 의사결정 트리, 랜덤 포레스트, 그래디언트 부스팅, **Voting 앙상블**
- 학습/테스트 분할, 스케일링, 특성 중요도 분석
- **Streamlit 대시보드**: 변동성 차트, 예측 확률, 성능 지표, CSV 다운로드
- PDF 보고서 생성 (ReportGenerator)
- 단위 테스트 (`tests/`)

---

## 프로젝트 구조

```
├── README.md
├── requirements.txt
├── main.py              # CLI: 학습(train) / 대시보드(streamlit)
├── run_app.py           # Streamlit 앱 실행
├── app.py               # Streamlit 대시보드 UI
├── data_loader.py       # 데이터 로드·검증 (MarketDataLoader)
├── preprocessor.py      # 특성 생성·스케일링·분할 (DataPreprocessor)
├── model.py             # 분류 모델·평가·저장 (VolatilityPredictor)
├── report_generator.py  # PDF 보고서 생성
├── docs/                # 구현 가이드, 설정 문서
└── tests/               # 단위 테스트
```

---

## 설치 및 실행

### 1. 의존성 설치

```bash
pip install -r requirements.txt
```

### 2. 모델 학습 (CLI)

```bash
python main.py --mode train --symbol AAPL --days 365 --model ensemble
```

`--model`: `logistic` | `dt` | `rf` | `gb` | `ensemble`

### 3. 대시보드 실행

```bash
python run_app.py
```

또는:

```bash
python main.py --mode streamlit
# 또는
python -m streamlit run app.py
```

### 4. 테스트 실행

```bash
python -m pytest tests/ -v
```

---

## 대시보드 구성

1. **설정 패널**: 주식 심볼, 분석 기간, 모델 선택
2. **변동성 차트**: 주가 변동성 시계열
3. **예측 차트**: 변동성 급증 예측 확률
4. **특성 중요도**: 모델별 특성 기여도
5. **모델 성능**: 정확도, 분류 보고서
6. **데이터 다운로드**: 결과 CSV

---

## 문제 해결

- Streamlit 실행 오류: `pip show streamlit` 로 설치 확인 후, 가상환경·Python 경로 확인
- 데이터 로드 실패: `data_loader`의 합성 데이터 옵션 사용 가능

---

## 라이선스

MIT License
