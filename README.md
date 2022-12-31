# AIOT-Final-Project T14 植基於深度學習之惡意軟體檢測

 
 此作業使用3種分類器 (ADAboost, XGBoost, Decision Tree) 針對惡意軟體做分類，分類Feature為軟體執行之Hardware Performance Counter (HPC)。  
 HPC資料如上，本次實驗使用trofold.xlsx，內有約6000筆HPC trace ，分別為2412筆正常軟體，與3279筆惡意軟之HPC trace。


# 執行流程
1. 開啟colab [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1qZwIZt70JjQvsyA23mm5RgxESS2tdpRa?usp=sharing)

2. import data  
    - trofold.xlsx  
    - 8test.xlsx  
    - 4P.xlsx    
  
3. 選擇HPC Feature  
    - 可選擇將不需要之HPC feature drop

  ```shell
from sklearn.model_selection import train_test_split
train_data, val_data = train_test_split(df, random_state=777, train_size=0.7)
print('訓練資料有%s筆' %len(train_data))
print('驗證資料有%s筆' %len(val_data))

X_train_df = train_data.drop(["class","L1-dcache-loads","L1-dcache-stores","branch-instructions","stalled-cycles-frontend"], axis=1) #,"L1-dcache-stores","dTLB-loads","L1-dcache-loads","branch-instructions"
X_train = np.array(X_train_df).astype(float)
Y_train_df = train_data['class']
Y_train = np.array(Y_train_df).astype(int)

X_valid_df = val_data.drop(["class","L1-dcache-loads","L1-dcache-stores","branch-instructions","stalled-cycles-frontend"], axis=1) #,"L1-dcache-stores","dTLB-loads"
X_valid = np.array(X_valid_df).astype(float)
Y_valid_df = val_data['class']
Y_valid = np.array(Y_valid_df).astype(int)
```  
  
4. 選擇分類器
    - XGBoost model  
    - AdaBoost model
    - Decision Tree model    
    
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
from sklearn.tree import DecisionTreeClassifier
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import classification_report
from sklearn.metrics import roc_curve, roc_auc_score, auc
import numpy as np
import time
ts = time.time()




# Confusion Matrix
mat = confusion_matrix(Y_valid, xg1_val)
sns.heatmap(mat,square= True, annot=True, cbar= False, fmt='d')
plt.xlabel("predicted value")
plt.ylabel("true value")
plt.show()

# Accuracy
accuracy = metrics.accuracy_score(Y_valid, xg1_val)
print('Valdation accuracy:', accuracy)

# precision, recall, f1-score
#target_names = ['0','1','2','3']
target_names = ['0','1']

print("report:\n",classification_report(Y_valid, xg1_val, target_names=target_names))

print('Total time took: {0}s'.format(time.time()-ts))

accuracy_score(Y_valid,xg1_val)
## Valdation accuracy: 0.8923076923076924
## Test accuracy: 0.41203281677301734
```
