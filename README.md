# AIOT-Final-Project T14 植基於深度學習之惡例軟體檢測
Using three type of classifier to handle Malware and benign software

 
 此作業使用3種分類器 (ADAboost, XGBoost, Decision Tree) 針對惡意軟體做分類，分類Feature為軟體執行之Hardware Performance Counter (HPC)
 HPC資料如上，本次實驗使用trofold.xlsx，內有約6000筆HPC trace ，分別為2412筆正常軟體，與3279筆惡意軟之HPC trace。


# 執行流程
1. 開啟colab連結 [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1qZwIZt70JjQvsyA23mm5RgxESS2tdpRa?usp=sharing)

2. import data
  -trofold.xlsx
  -8test.xlsx
  -4P.xlsx
  
3. 選擇HPC Feature
 　```shell
  X_train_df = train_data.drop(["class","L1-dcache-loads","L1-dcache-stores","branch-instructions","stalled-cycles-frontend"], axis=1) #,"L1-dcache-stores","dTLB-loads","L1-dcache-loads","branch-instructions"
  ```
4. 選擇分類器 (XGBoost model,AdaBoost model,Decision Tree model)

5. 訓練Model 
 　```shell
  xg1=xg1.fit(X_train, Y_train)
  ```
6. 預測
 　```shell
  xg1_val=xg1.predict(X_valid)
  ```
  
7. 分析結果
 　```shell
  accuracy = metrics.accuracy_score(Y_valid, xg1_val)
  ```
