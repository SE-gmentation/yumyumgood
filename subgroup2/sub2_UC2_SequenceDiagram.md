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

2. (매번)크롤링 or DB에 메뉴 저장
=> 메뉴 정보를 항상 사용하고 메뉴에 따른 정보를 수정하기 때문에 **디비에 저장**해놓는 것이 효율적이다.

3. 판매 메뉴가 냠냠굿 메뉴 목록에 존재하지 않는 경우
=> 이는 크롤링 모듈이 책임져야할 부분임. 따라서 이번 과제에서는 모든 판매메뉴가 메뉴 상태관리에 존재한다고 가정함.

<hr/>

## Variation 1

### Variation 1a
![image](https://user-images.githubusercontent.com/65646971/118356282-5c74e100-b5af-11eb-88e4-ebf8cffbf816.png)

<br/>

### Variation 1b
![image](https://user-images.githubusercontent.com/65646971/118356284-61d22b80-b5af-11eb-9d1c-b905778ff6de.png)

### 고민 사항
어쩌구

### 수정 결과
이 근거로 어쩌구

<hr/>

## Variation 2

### Variation 2a
![image](https://user-images.githubusercontent.com/65646971/118356284-61d22b80-b5af-11eb-9d1c-b905778ff6de.png)

<br/>

### Variation 2b
![image](https://user-images.githubusercontent.com/65646971/118356329-baa1c400-b5af-11eb-9861-569559465a42.png)

### 고민 사항
어쩌구저쩌구

### 수정 결과
이렇게하기루함~

<hr/>

## Final Sequence Diagram

![image](https://user-images.githubusercontent.com/65646971/118356353-dc9b4680-b5af-11eb-8142-af665f2ccff2.png)