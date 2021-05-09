모델 비교

1. 시계열 transformer > for stock prediction

https://towardsdatascience.com/stock-predictions-with-state-of-the-art-transformer-and-time-embeddings-3a4485237de6

https://colab.research.google.com/drive/1lN4V3mC5WYogawsHbdYnue_U1cqHEGbE#scrollTo=G3plS9BcUS5w



> Inception 구조 관련한자료:  http://datacrew.tech/inception-v4-2016/ 


MAE, MAPE, 

*Weighted Absolute Percentage Error (WAPE)*





======================================================= </br>
data = grx.us 

- tramsformer ---> **O**

  Evaluation metrics
  raining Data - Loss: 0.0017, MAE: 0.0255, MAPE: 6.9180
  Validation Data - Loss: 0.0006, MAE: 0.0187, MAPE: 4.8767
  Test Data - Loss: 0.0002, MAE: 0.0117, MAPE: 3.0283

- tramsformer - moving average ---> 다시

  - 1차 (volumn 에 df_cal 아니라 df로 적용함) ---> **O**
    Evaluation metrics
    Training Data - Loss: 0.0015, MAE: 0.0265, MAPE: 6.1947
    Validation Data - Loss: 0.0007, MAE: 0.0207, MAPE: 4.0275
    Test Data - Loss: 0.0003, MAE: 0.0146, MAPE: 2.7811

  - 2차 ------> **X**
    Evaluation metrics
    Training Data - Loss: 0.0051, MAE: 0.0504, MAPE: 12.1804
    Validation Data - Loss: 0.0019, MAE: 0.0343, MAPE: 6.4099
    Test Data - Loss: 0.0011, MAE: 0.0268, MAPE: 5.1966

- Bi-LSTM ------> **X**
  Evaluation metrics
  Training Data - Loss: 0.0018, MAE: 0.0269, MAPE: 7.1447
  Validation Data - Loss: 0.0006, MAE: 0.0197, MAPE: 5.0383
  Test Data - Loss: 0.0003, MAE: 0.0135, MAPE: 3.4425

- cnn + bi-lstm ---> **X/O**
  Evaluation metrics (checkpoin saved)
  Training Data - Loss: 0.0017, MAE: 0.0256, MAPE: 6.9206
  Validation Data - Loss: 0.0006, MAE: 0.0186, MAPE: 4.8305
  Test Data - Loss: 0.0003, MAE: 0.0120, MAPE: 3.0839

- (cnn + bi-lstm) ---> **X/O**
  Evaluation metrics (model saved)
  Training Data - Loss: 0.0017, MAE: 0.0258, MAPE: 6.9084
  Validation Data - Loss: 0.0006, MAE: 0.0194, MAPE: 5.0361
  Test Data - Loss: 0.0003, MAE: 0.0120, MAPE: 3.1206


- LSTM ---> **X/O**
  Evaluation metrics
  Training Data - Loss: 0.0017, MAE: 0.0261, MAPE: 7.0149
  Validation Data - Loss: 0.0006, MAE: 0.0190, MAPE: 4.9015
  Test Data - Loss: 0.0003, MAE: 0.0121, MAPE: 3.1110
  
  
- LSTM (MV *sigmoid로 activation 변경 X*) ---> **X**
  Evaluation metrics
  Training Data - Loss: 0.0035, MAE: 0.0402, MAPE: 9.9064
  Validation Data - Loss: 0.0018, MAE: 0.0319, MAPE: 6.3062
  Test Data - Loss: 0.0007, MAE: 0.0217, MAPE: 4.1799
