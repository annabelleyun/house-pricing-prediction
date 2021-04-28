# research-house-pricing



참고
LSTM
https://roboreport.co.kr/%eb%94%a5%eb%9f%ac%eb%8b%9dlstm%ec%9c%bc%eb%a1%9c-%ec%95%84%ed%8c%8c%ed%8a%b8-%ec%a7%80%ec%88%98-%ec%98%88%ec%b8%a1%ed%95%98%ea%b8%b0-1-%ed%9b%88%eb%a0%a8-%eb%8d%b0%ec%9d%b4%ed%84%b0-%ec%83%9d/
LR
https://roboreport.co.kr/scikit-learn%ec%9d%84-%ec%82%ac%ec%9a%a9%ed%95%98%ec%97%ac-%eb%b6%80%eb%8f%99%ec%82%b0-%ea%b0%80%ea%b2%a9-%ec%98%88%ec%b8%a1%ed%95%98%ea%b8%b0-4-linear-regression-%ec%82%ac%ec%9a%a9%eb%b2%95/

## Dataset

1. 한국감정원의 전국주택가격 지수 (매주/월간으로 전국 아파트, 단독, 연립주택을 표본 조사해서 하나의 수치로 만든수치 > 주택시장의 평균적인 가격변화를 측정하는 지표로 사용됨)
> R-ONE 부동산통계정보 바로가기(http://www.r-one.co.kr/rone/resis/common/sub/sub.do?pageVal=page_2_2)
 - 주택 종합 및 아파트 : 176개 시군구(78시, 8군, 101구)
 - 연립 및 단독주택 : 17개 시도 및 생활권역
 - 21.1월 공동주택 실거래가격지수 공표용 보고서_최종.pdf

2. 외부변수 추가(금리/환율 등)
3. 정책긍/부정지수 추가

## Data Cleansing


## Proposed Model
- Transformer (attention) 기반

### Experiments

## Baseline
- LR
- Lasso
- Elastic
- Kernel Gradient
- LSTM
- XGBoost
- LGBM

## Training


## Validation

ACC:
- MAE
- MSE
- RMSE

Experimental Setup
Model Structure
Experiment Result

## Prediction


## Conclusion
