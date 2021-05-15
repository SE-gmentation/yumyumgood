# [UC2] Sequence Diagram

> 20193057 김승아, 20190323 배인경

<hr/>

## 목차

#### [1. Initial Sequence Diagram](#Initial-Sequence-Diagram)

#### [2. Variation 1](#Variation-1)

#### [3. Variation 2](#Variation-2)

#### [4. Final Sequence Diagram](#Final-Sequence-Diagram)


<hr/>

## Initial Sequence Diagram

![image](https://user-images.githubusercontent.com/65646971/118356222-20da1700-b5af-11eb-9aaa-ff9c096e355f.png)

### 고민 사항
1. 메뉴 관리키 선택 시 해당 메뉴 정보를 조회하기 위해 현재 날짜, 유저의 담당식당 정보가 필요하다. <br/>
=> **날짜처리기, 유저 정보 처리기** 를 통해 현재 정보 처리

2. (매번)크롤링 or DB에 메뉴 저장 <br/>
=> 메뉴 정보를 항상 사용하고 메뉴에 따른 정보를 수정하기 때문에 **디비에 저장**해놓는 것이 효율적이다.

3. 판매 메뉴가 냠냠굿 메뉴 목록에 존재하지 않는 경우 <br/>
=> 이는 크롤링 모듈이 책임져야할 부분임. 따라서 이번 과제에서는 모든 판매메뉴가 메뉴 상태관리에 존재한다고 가정함.

4. 수정하기 상태에서 정보/수량 수정 박스 클릭 시 label -> text로 변경 <br/>
=> 정보 부분을 수정하는 컴포넌트를 재구성하는 모듈을 넣나 pagemaker가 다시 반영해야 하나 고민하였으나 사용자의 화면구성도 바로바로 바뀌어야하기 때문에 **pagemaker**가 매번 작동되어야 한다.

5. 판매 상태와 , 판매 수량 정보를 어떻게 함께 받을 것인가? <br/>
- 판매 상태 수정 중인 지/ 재고 준비량 수정 중인 지를 처음부터 구분해서 수정 작업하기
- 수정 작업하기 상태라고 인식만 되면 판매상태와 재고준비량을 모두 한 번에 바꾸기 <br/>
=> bool / int형으로 자료형이 다르므로 다르게 처리해야함.

<hr/>

## Variation 1

### Variation 1a
![image](https://user-images.githubusercontent.com/65646971/118356282-5c74e100-b5af-11eb-88e4-ebf8cffbf816.png)

<br/>

### Variation 1b
![image](https://user-images.githubusercontent.com/65646971/118356284-61d22b80-b5af-11eb-9d1c-b905778ff6de.png)

### 고민 사항
1. Status 정보 수정 후 getter & setter 함수 수행 시점 <br/>
- 컨트롤러에서 status = getStatus(menu)를 통해 현재 상태를 받아와 현재 상태가 pos/neg면 neg/pos로 변수 status 값을 바꿈. DB에 수정 된 상태를 저장하는 시점은 **저장하기** 버튼을 클릭 했을 때 전체 메뉴에 대해 setStatus(menu, status)를 for문으로 수행하여 Edit Checker를 통해 DB에 변한 내용 저장 <br/>
- 컨트롤러에서 status = getStatus(menu)를 통해 현재 상태를 받아와 현재 상태가 pos/neg면 neg/pos로 변수 status 값을 바꿈. 해당 상태를 바로 setStatus(menu, status)를 수행하여 Database Connection에 수정 사항을 반영함. 최종적으로 저장하기 버튼을 클릭했을 때 Database Connection에서 save()로 저장되어 있던 수정 사항들을 받아서 디비를 수정함. <br/>

2. Amount 정보 수정 후 getter & setter 함수 수행 시점 <br/>
- 컨트롤러에서 amount = getAmount(menu)를 통해 현재 상태를 받아와 변수 amount 값을 새로 입력된 값인 a로 바꿈. DB에 수정 된 상태를 저장하는 시점은 **저장하기** 버튼을 클릭 했을 때 전체 메뉴에 대해 getAmount(menu, amount)를 for문으로 수행하여 Edit Checker를 통해 DB에 변한 내용 저장 <br/>
- 컨트롤러에서 amount = getAmount(menu)를 통해 현재 상태를 받아와 변수 amount 값을 새로 입력된 값인 a로 바꿈. 해당 상태를 바로 setAmount(menu, amount)를 수행하여 Database Connection에 수정 사항을 반영함. 최종적으로 저장하기 버튼을 클릭했을 때 Database Connection에서 save()로 저장되어 있던 수정 사항들을 받아서 디비를 수정함. <br/>


### 수정 결과
기존에 존재하던(Variation 1a) 🙂Edit Checker의 응집도가 지나치게 낮아 Edit Checker를 삭제함. 또한 for문으로 모든 정보를 마지막에 save()함수로 Edit Checker를 통해 DB에 내용을 저장하면 수정되지 않은 사항에 대해서도 save() 작업을 다시 해줘야하므로 비효율적이라고 판단함.<br/>
=> **Variation 1b**로 수정

<hr/>

## Variation 2

### Variation 2a
![image](https://user-images.githubusercontent.com/65646971/118356284-61d22b80-b5af-11eb-9d1c-b905778ff6de.png)

<br/>

### Variation 2b
![image](https://user-images.githubusercontent.com/65646971/118358791-74eaf880-b5bb-11eb-8f2b-4f7f2b10cf07.png)

### 고민 사항
1. DB에 수정사항들을 save()하는 시점 <br/>
- 마지막에 save button을 클릭했을 때(Variation 2a)<br/>
- 상태나 양을 변화하는 textbox를 각각 클릭하고 값을 수정할 때 마다(Variation 2b)<br/>

### 수정 결과
Variation 2a처럼 🙂Controller에서 save()함수를 수행한 후 🙂Database Connection에서 saveData() 함수를 실행한 후 최종적으로 DB내용을 수정하는 과정을 거치면 결합도가 높다고 판단함. 그러므로 Varition 2b처럼 각 setter함수 수행 시점에 바로 saveStatus()/saveAmount() 함수를 실행하여 DB내용을 수정하고 save button을 클릭했을 때는 페이지 랜더링만 다시 수행되도록 수정함.<br/>
=> **Variation 2b**로 수정

<hr/>

## Final Sequence Diagram

![image](https://user-images.githubusercontent.com/65646971/118362899-b2a44d00-b5cc-11eb-8784-2f4acc9b7ef2.png)