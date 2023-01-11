# Big Data-Final-Project T13 電影喜好預測期末專案

 
   - 此作業使用KNN之方法，先找出與預測目標喜好最相符的ID (high correlation)將相似的ID對預測結果填值
   - 本次使用Training Dataset 分別為 'movies.xlsx' 'ratings.xlsx' 'users.xlsx'
   - Predict Dataset 為 teachers_rating


# 執行流程
1. 開啟colab [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1ToCij4TfVhnGvrqGEObNegzTDwZjVCwt?usp=sharing)

2. Import data  
    - movies.xlsx
    - ratings.xlsx
    - users.xlsx 
3. Import teachers_rating

4. KNN 尋找最相近之使用者 
    - 可調整count數量來選擇接近程度

  ```shell
for i in range (len(ratings['	user_id	movie_id	rating	timestamp	user_emb_id	movie_emb_id'])):
  temp = ratings['	user_id	movie_id	rating	timestamp	user_emb_id	movie_emb_id'][i]
  temp_list = temp.split()
  if(temp_list[1] != str(id)): 

    count = 0
    for j in range (3953):
      if(teacher_rating[j] != 0 and teacher_rating[j]==id_rating[j]):
        count += 1

    if(count>8):
      print(id_rating)
      print(id)
      for k in range (len(teacher_unrateing)):
        if(id_rating[teacher_unrateing[k]] != 0):
          rating_nb[teacher_unrateing[k]] += id_rating[teacher_unrateing[k]]
          rating_count[teacher_unrateing[k]] += 1
        print(teacher_unrateing[k])
        print(id_rating[teacher_unrateing[k]])


  
    clean_array(id_rating)
    i = i - 1
    id = id + 1
  else:
    id_rating[int(temp_list[2])] = int(temp_list[3])

```  
  
5. 選出相近的使用者進行Predict
    - 加總並除權重  
  ```shell
for i in range (len(teacher_unrateing)):
  a = rating_nb[teacher_unrateing[i]]
  b = rating_count[teacher_unrateing[i]]
  print(teacher_unrateing[i])
  print(a/b)
```  
    
6. 輸出預測結果   
  ```shell
ID     point
253  : 4.0
527  : 5.0
260  : 5.0
3623 : 4.5
3793 : 4.5
2571 : 4.5
3510 : 5.0
3273 : 3.0
208  : 3.5
3409 : 3.5
``` 



