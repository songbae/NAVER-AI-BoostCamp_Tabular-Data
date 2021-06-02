
### 📜 온라인 상점 구매 예측 Competition

##### 본프로젝트는 🚀NAVER AI BoostCamp에서 개최한 competition입니다
##### 📆 2021.04.12 ~ 2021.04.23
#### 🏆최종결과 Public Score : 0.8605 16등

---
### 👀 문제 정의 및 해결 방법

- Tabular Data라는 task에서 어떤식으로 접근하고 , 학습하고, 최종적으로 사용한 솔루션에 대해서는 [report](https://songbae.oopy.io/8ced5f47-6afe-4bc6-9228-fb84fad7e094)에서 !


### 💡[대회 정보]

- 주어진 Data의 feature들을 이용해서 다음 달 소비자들이 300$이상을 소비 유무를 예측하는 Competion이었습니다
- Data 컬럼 설명
    -  order_id=주문번호, 데이터에서 같은 주문번호는 동일 주문을 나타냄
    -  product_id: 상품 번호 
    -  description: 상품 설명 
    -  quantitiy: 상품 주문 수량 
    -  order_data: 주문 일자 
    -  Price: 상품 가격 
    -  customer_id: 고객 번호 
    -  country: 고객 거주 국가 
    -  total : 총구매액 
   
#### 💡[Environment]
---
- Window 10
- VsCode
- GPU-p40
- Python, Notebook

#### 📑Code 구조

```
C:.
│  README.md
│  requirements.txt          ### 실행에 필요한 모듈 
│
├─input
│      sample_submission.csv  
│
└─src
    │  evaluation.py        ### Train 및 valid 
    │  features.py          ### Train에 필요한 feature 추가/삭제
    │  inference.py         ### inference (submission )
    │  model.py             ### model -> xg_boost, NN, light-gbm 
    │  utils.py             ###그 외 필요한 function

```
 ---
 
### inference.py
```
~$ python infernence.py --model --num_features --hidden_size --batch_size --seed 
```
### args:
  - model: [light_bgm, nn_model ,type=str, default=light_bgm] 
  > select which model to use 

  - num_features: [type=int , default=55] 
  > select feature nums 

  - hidden_size: [type=int, default=1024] 
  > how many nodes to use in hidden layer 

  - batch_size:[type=int, defalut=512] 
  > select batch_size

  - seed:[type=int, default=777] 
  > seed num for reproduction 

--- 

### utils.py 
  - seed_everything
  > set seed for reproduction

  - print_score
  > matric for evaluating score 
  - make_product_month
  > make obj-> numeric tpye of product_id with group_by month
  - make_month_over_train_300
  > feature extraction by bins of 3,6,9,20 month with groupby [customer_id ,year_month] ratio of over 300$
  - make_month_over_test_300
  > same with above but using year_month 2011-11
  - make_time_corr_train
  > feature extraction by bins of order_data 

  - make-time _corr_train
  > same with above
---
### features.py 

- generate_label
```
return label
```
> making labels by 2011-11 
- make_feature 
```
return x_tr, x_te
```
> transform obj-> numeric tpye and fill None values with Median values 
- feature_engineering1
```
return : x_tr, x_te, all_train_data['label'],features
```
> adding features and agg function for features 



