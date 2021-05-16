## Multi-Head Self Attention 기반 아파트 매매지수 예측

Keywords: Transformer, Self-Attention, NLP, Time Series Prediction, Real-Estate Index


## Goal

Transformer Encoder구조를 Time Series 데이터에 활용하여 부동산 매매가격 변동을 예측하는데 활용하고자 함.

**실험 목표 1)** 실험을 통해 Transformer 구조가 시계열 데이터를 다루는 데에도 충분한 가능성이 있음을 보여주고자 함. (+ Time2Vec)
(*선행연구에서 인공신경망 모델(RNN, LSTM)과 전통적인 통계 모형(다중 회귀모형, ARIMA와 VAR 등)의 예측력 비교 분석을 통해 인공신경망 모형의 우수성을 실증적으로 검증함)

**실험 목표 2)**  Multi-head Self-Attention을 활용하여 각  time-step에서 다변량 예측모델이 각 변수들의 관계를 잘 살펴보고 학습 결과를 예측에 반영할 수 있게 함

**실험 목표 3)** LSTM+Time2Vec 을 통한 예측모델 확인 및 Dataset 구성 (Transformer Encoder + Time2vec 구조가 학습에 효과가 없는 경우)


## Dataset

### 2021.05.17 Dataset_v2.0
2006.01 ~ 2021.02 월별 아파트 실거래가격지수 (서울지역/규모별)
+ 가계대출액(https://ecos.bok.or.kr/EIndex.jsp) (가계신용>가계대출>주택담보대출&기타대출)

> ![image](https://user-images.githubusercontent.com/49928736/118402031-139e5480-b6a3-11eb-8499-a80988c2fc5c.png)

### Dataset 참고자료

1. 한국감정원의 전국주택가격 지수 (매주/월간으로 전국 아파트, 단독, 연립주택을 표본 조사해서 하나의 수치로 만든수치 > 주택시장의 평균적인 가격변화를 측정하는 지표로 사용됨)
> R-ONE 부동산통계정보 바로가기(http://www.r-one.co.kr/rone/resis/common/sub/sub.do?pageVal=page_2_2)
 - 주택 종합 및 아파트 : 176개 시군구(78시, 8군, 101구)
 - 연립 및 단독주택 : 17개 시도 및 생활권역
 - 21.1월 공동주택 실거래가격지수 공표용 보고서_최종.pdf

2. 외부변수 추가(금리/환율 등)

3. 정책긍/부정지수 추가

4. 데이터 Feature 참고 (https://roboreport.co.kr/scikit-learn%ec%9d%84-%ec%82%ac%ec%9a%a9%ed%95%98%ec%97%ac-%eb%b6%80%eb%8f%99%ec%82%b0-%ea%b0%80%ea%b2%a9-%ec%98%88%ec%b8%a1%ed%95%98%ea%b8%b0-4-linear-regression-%ec%82%ac%ec%9a%a9%eb%b2%95/)

> 추가 가능한 리스트
> - 매매가격지수(시도별): tradeprice_sido_n1
> - 날짜: date, 연도: year, 월: month
> - 지역코드(시도): region_cd
> - 매매가격지수(시도): tradeprice_sido
> - 부동산타입:	building_type
> - 건설기성액(백만원)	: construction_realized_amount
> - cd 금리	: cd
> - 정기예금금리	: spirit_deposit_rate
> - 환율	: exchange_rate
> - 종합주가지수	: composite_stock_price_index
> - 경제성장률	: economy_growth
> - 국고채3년	: exchequer_bond_three
> - 가계대출액(전국)	: household_loan_all
> - 주택대출액(전국)	: mortgage_all
> - 미분양 가구수(시도)	: numberofnosells
> - 공사완료후 미분양(민간,시도) : unsalenum_c 


## Data Cleansing / EDA

- Min-Max Normalization
- 8:1:1 = train:test:validation

> missing data에 대해 생각할 때 중요한 질문
> - missing data가 얼마나 보편적인가?
> - missing data가 랜덤인가? 패턴이 있는가?
> - ROW를 삭제할 것인가 대체할 것인가?

## Proposed Model
- Transformer Encoder (Multi-head Self Attention) (>>> Decoder 추가 실험 필요)
+ Time Embedding: Time2Vec (시간의 주기성& 불변성 표현)
![image](https://user-images.githubusercontent.com/49928736/118404363-95937b00-b6ad-11eb-8012-3bfb08008e91.png)



### Experiments
- Experimental Setup
- 실험 내용 (진행사항 일자별 업데이트 예정)

## Model Comparison
- Linear Regression (Baseline #1)
- Lasso
- Elastic
- Kernel Gradient
- LSTM (Baseline #2)
- XGBoost
- LGBM
- Transformer Encoder (Baseline #3)
- Transformer Encoder + Time2Vec (and & Moving Average)
- CNN+LSTM (and & Moving Average)
- BI-LSTM (and & Moving Average)
- LSTM + Time2Vec (and & Moving Average)

## Training & Validation

Accuracy(Loss):
- MAE, MAPE
- MSE, RMSE


## Prediction
- 실험결과 표
- 예측값 vs 실제값 비교 그래프

## Conclusion

### Future work
Social Embedding : 부동산 정책에 대한 긍/부정 지수 추가
> 단기예측 / 최근 3개월간 기사, 여론조사 크롤링을 통해 수집
