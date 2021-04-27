# research-house-pricing


## Idea 
코로나 이후 상항에 대한 집값 예측

참고
https://roboreport.co.kr/scikit-learn%ec%9d%84-%ec%82%ac%ec%9a%a9%ed%95%98%ec%97%ac-%eb%b6%80%eb%8f%99%ec%82%b0-%ea%b0%80%ea%b2%a9-%ec%98%88%ec%b8%a1%ed%95%98%ea%b8%b0-4-linear-regression-%ec%82%ac%ec%9a%a9%eb%b2%95/

## Dataset

1. 한국감정원의 전국주택가격 지수 (매주/월간으로 전국 아파트, 단독, 연립주택을 표본 조사해서 하나의 수치로 만든수치 > 주택시장의 평균적인 가격변화를 측정하는 지표로 사용됨)
> R-ONE 부동산통계정보 바로가기(http://www.r-one.co.kr/rone/resis/common/sub/sub.do?pageVal=page_2_2)
 - 주택 종합 및 아파트 : 176개 시군구(78시, 8군, 101구)
 - 연립 및 단독주택 : 17개 시도 및 생활권역
 - 21.1월 공동주택 실거래가격지수 공표용 보고서_최종.pdf

2. 외부변수 추가(금리/환율 등)
3. 정책긍/부정지수 추가

## Baseline
- LR
- LSTM
- XGBoost

## Proposed Model
- Transformer (attention) 기반

### Experiments



## Data Cleansing


## Training


## Validationcc

ACC 지표
- MSE
- RMSE

## Prediction


## Conclusion
