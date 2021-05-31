## 📢 SubGroup 3

- 주제 소개 
  - 식당 이용자의 리뷰 관련 기능 주제를 맡은 SUBGROUP3 박지수[jisoo-o](https://github.com/jisoo-o/)/이주연[2JooYeon](https://github.com/2JooYeon) 입니다. 
  - 총 5가지의 USE-CASE 중 UC-2, UC-4의 기능을 구현하였고, UC-3, UC-5는 부분적으로 구현하였습니다. 
  - UC-2 : 학식 건물 별 평점 확인
  - UC-4 : 리뷰 작성
  - (UC-3 : 리뷰 확인, UC-5 : 주문 내역 )


- 개발한 기능 
  - 식당 이용자의 주문 내역 열람, 리뷰 작성 기능 구현
  - opinion mining을 이용한 리뷰의 긍정 또는 부정 확률 계산 기능 구현 

<br/>

## 🔨 Tech stacks & Language


- Kotlin, Java, Python3
- Android Studio
- Tensorflow, Mecab

<br/>

## 🔎 Getting Started

Default. Clone this repository

   ```bash
   $ git clone https://github.com/SE-gmentation/yumyumgood_subgroup3
   ```
   
- Android App 실행 방법

1. Change the directory 

   ```bash
   $ cd YumyumgoodApp
   ```

2. Open with Android studio and run AVD emulator
<br/>

- 리뷰 감정 분석 실행 방법

1. Change the directory

   ```bash
   $ cd Review_SentimentAnalysis
   ```
2. Open **Sentiment_analysis.ipynb** with Google Colab
<br/>


## 📸 Features & Demo Screenshot
![logo (1)](https://user-images.githubusercontent.com/69567269/120076519-dbeece00-c0e0-11eb-8517-0f244a3ecdc1.png)      

- **( UC-5 ) 주문 내역 열람**
  - 식당 이용자의 주문 내역을 시간 순으로 정렬하여 보여준다. 주문 내역은 학식당, 주문한 메뉴, 결제 금액, 경과일을 포함한다.     
각 내역 별 3개의 버튼, 1.리뷰 작성 2.주문 상세 3.식당 보기 가 존재한다. 리뷰 작성 버튼은 *Domain Model 의 concept "카운터"* 가 작용한다.      
주문한지 3일이 지나면 버튼이 비활성화되어 리뷰를 작성할 수 없고 작성 기간을 경과하였음을 알린다.</br>           
![주문내역](https://user-images.githubusercontent.com/69567269/120077520-b617f800-c0e5-11eb-95b4-64eb26dad28d.png)     
      
---

- **( UC-4 ) 리뷰 작성**
  -  식당 이용자는 주문한 각 메뉴에 대하여 추천 여부를 버튼을 통해 남기고, 메뉴와 식당 시설에 대한 전반적인 리뷰를 최소 5자 최대 300자 내로 남길 수 있다. *Domain Model 의 concept "리뷰 당위성 확인"* 이 모든 메뉴에 대한 추천 여부를 선택하였는지와 글자수 조건을 만족하였는지 확인하여 리뷰 제출을 가능하게 해준다. 글자수는 changeListener를 이용하여 실시간으로 반영된다.     
조건을 만족하지 못하면 case 1. 추천 여부 미선택 시 dialog 안내, case 2. 최소 5자 이상 작성하지 않았을 시 dialog 안내, case 3. 300자 초과 시 입력 불가로 조건 만족을 유도한다.</br>  
![리뷰작성진입](https://user-images.githubusercontent.com/69567269/120077531-c4feaa80-c0e5-11eb-9021-62b0f95f1214.png)![추천안함](https://user-images.githubusercontent.com/69567269/120077561-e8c1f080-c0e5-11eb-930e-6ba2fc170150.png)        
![5자미만](https://user-images.githubusercontent.com/69567269/120077559-e495d300-c0e5-11eb-9f27-896c2afeb301.png)
![제출가능](https://user-images.githubusercontent.com/69567269/120077573-ff684780-c0e5-11eb-9792-47d6f26efcf0.png)

---

- **( UC-2, 3 ) 식당 보기 : 식당 평점 및 다른 이용자의 리뷰**
  -  식당 이용자는 다른 이용자들이 해당 학식당에 남긴 리뷰들과 그로부터 계산된 총점을 한눈에 확인할 수 있다. 리뷰 평점 계산은 opinion mining을 통해 이루어진다. 사용자가 남긴 리뷰는 긍정 또는 부정의 리뷰로 구분지어진다. 이때 구분의 정확도로 확률이 함께 계산되는데 해당 확률을 가중치로 리뷰는 수치화 된다. 예를 들어 확률의 10퍼센트 단위로 단계를 나누어 단계별로 부여하는 점수를 다르게 줄 수도 있을 것이다. 긍정 리뷰의 90퍼센트 이상은 10점으로, 80-90퍼센트는 9점.. 또는 부정 리뷰의 90퍼센트 이상은 1점으로, 80-90퍼센트는 2점.. 등의 방식으로 치환하는 과정을 거칠 수 있을 것이다. 특정 학식 건물의 모든 리뷰가 수치화되면 전체 리뷰의 수치화된 점수의 총합을 전체 리뷰 개수로 나눈 평균을 계산할 수 있을 것이다. 해당 평균점수의 구간에 따라 "최고에요", "맛있어요", "아쉬워요" 등의 문구로 식당의 평점을 나타낼 수 있고, 해당 문구는 사용자가 보는 앱 페이지에 뜨게 된다.</br>      
![식당보기](https://user-images.githubusercontent.com/69567269/120077647-60901b00-c0e6-11eb-8e7e-cced2aadcfa3.png)    

---

- **( UC-2 ) 학식 건물별 평점 확인**
  -  사용자가 작성한 리뷰는 opinion mining을 이용하여 몇 퍼센트의 확률로 긍정 또는 부정의 리뷰인지 구분된다. 리뷰 감정분석을 위한 데이터를 얻기 위해 네이버의 맛집 리뷰를 selenium을 이용해서 동적으로 크롤링 했다. 총 14군데의 식당의 리뷰를 크롤링한 결과로 대략 9500개의 데이터가 생성되었다. 네이버 리뷰에서 리뷰 텍스트 뿐만 아니라 작성자가 남긴 평점도 크롤링하였는데, 평점이 4, 5인 리뷰들에 긍정을 의미하는 레이블 1을 부여하고, 평점이 1, 2인 리뷰들에 부정을 의미하는 레이블 0을 부여하여 감성 분류를 수행하는 모델을 만들었다. 참고로 3점인 리뷰는 긍정과 부정을 확고히 나누기 애매하다고 생각하여 제외했다. 
  -  형태소 분석기로는 Mecab을 사용하였고, 본인의 노트북에 설치하는데에 오류가 있어서 편리하게 사용하기 위해 Google Colab을 이용해서 설치했다.
  -  리뷰 기반의 감정 분석을 하기 위해 GRU 모델을 이용했다. 
  -  아래 사진은 사용자가 리뷰를 입력했다고 가정하고, 감정 분석의 결과를 테스트한 결과이다. </br>   
![감정분석 결과보기](https://user-images.githubusercontent.com/48883581/120184220-ae726380-c24b-11eb-9b54-f4bbcfccf70b.png)

---

## 📍 SSD(Class Diagram) 대조표

>   | 클래스명(함수명) |  SSD 내 컨셉(클래스)이름  |
>   | --- | ---  |
>   |**Sentiment_analysis.ipynb** | 리뷰수치화 (UC-2 학식 건물 별 평점확인)|
>   |**class OrderHistory - btnWriteReview.isEnabled** | 카운터 (UC-4 리뷰 작성)|
>   |**class WriteReview - submit_button.setOnClickListener, write_review.addTextChangedListener** | 리뷰 당위성 확인 (UC-4 리뷰 작성)|
>   |**class WriteReview - showDialog()** | 디스플레이 (UC-4 리뷰 작성)|
>   |**class WriteReview - showErrorDialog(), showSelectLike()** | 예외페이지 생성 (UC-4 리뷰 작성)|
>   |**class ViewBuilding** | (UC-3 리뷰 확인)|
>   |**class OrderHistory** | (UC-5 주문내역 확인)|
  
<br/>

## 💻 참고사항
- 코드 작업 위치 : yumyumgood_subgroup3 respository
- 추후 안드로이드 앱 식당보기 뷰에서 리뷰 감정분석 알고리즘의 결과값을 확인할 수 있도록 연동하여 구현할 예정 
<br/>

## 🤣 개선사항
- 사용자가 작성한 리뷰를 감정분석하기 위한 opinion mining에서 기계학습을 위한 데이터로 네이버 맛집 리뷰를 크롤링 해서 이용했는데, 긍정 레이블인 1에 대응하는 리뷰의 수와 부정 레이블인 0에 대응하는 리뷰의 수 차이의 불균형이 심했기 때문에 이를 해결하기 위해 수가 더 적은 부정 레이블에 해당하는 리뷰의 수를 기준으로 샘플링을 진행해서 데이터의 수가 줄어드는 결과가 발생했다. 데이터의 수가 줄어들다 보니 학습에 충분한 데이터가 돌아가지 못했고 그에 따라 정확도가 떨어지는 결과를 가져왔다. 따라서 추후에 긍정과 부정의 리뷰가 균형적으로 존재하는 대량의 데이터를 기반으로 학습시킨다면, 알고리즘의 정확도를 높일 수 있을 것이라고 기대한다. 
