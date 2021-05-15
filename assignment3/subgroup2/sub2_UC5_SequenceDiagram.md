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

![uc5](https://user-images.githubusercontent.com/52988414/118357468-52ee7780-b5b5-11eb-9e57-86a5f6e54e57.png)

<hr/>

## Variation 1

![class-Page-2](https://user-images.githubusercontent.com/52988414/118362459-88519000-b5ca-11eb-930b-8072e8da5e19.png)

### 고민 사항

DB에게 날짜 정보를 보내 커뮤니케이션하는 수행은 날짜 컨트롤러가 아닌 메뉴관리 컨트롤러에서 수행하는 것이 높은 응집도를 갖고 설계 목적에 적합한다고 판단했다. 날짜 컨트롤러는 날짜 계산과 캘린더 모달 생성을 통해 날짜 정보를 컨트롤러에게 전달하는 역할을 수행하는 것에 집중하도록 재설계 했다.

### 수정 결과

DB연결과 DB에 관한 사항은 배제하여 컨트롤러로 날짜 정보를 전달하도록 구조를 설계했다.

<hr/>

## Variation 2

월 변경 버튼
![image](https://user-images.githubusercontent.com/52988414/118362711-9bb12b00-b5cb-11eb-9123-7a6042bc20fc.png)
일 변경 버튼
![image](https://user-images.githubusercontent.com/52988414/118362724-a370cf80-b5cb-11eb-93d6-a119b657d481.png)

### 고민 사항

버튼인터페이스에서 월, 일을 조회할 수 있는 <, > 버튼을 각각 확인하여 work 함수로 컨트롤러에게 변화값을 전달했다. 하지만 버튼 인터페이스에서 월, 일 버튼인지 먼저 확인한 후 변화값을 delta라는 변수에 담아 전달하는 것이 버튼 객체의 구조에 적합하고 컨트롤러의 부하를 낮출 수 있다고 판단했다.

### 수정 결과

![class-Page-3](https://user-images.githubusercontent.com/52988414/118362457-87b8f980-b5ca-11eb-9660-b2585ee67be7.png)

## Variation 3

![image](https://user-images.githubusercontent.com/52988414/118362858-7a047380-b5cc-11eb-8b4b-f0f2ee740159.png)

### 고민 사항

초기 시퀀스 다이어그램에서는 날짜계산기가 날짜정보를 바탕으로 캘린더를 구성해서 html 모달을 생성하도록 했다. 그런데 날짜계산기가 다른 객체에 비하여 많은 일을 하는 것을 고민했다. 비중도 밸런스를 고려하여 캘린더생성기 객체를 만들고 날짜 정보를 받아 리스트 자료형으로 캘린더를 구성하여 모달생성기로 전달하는 설계를 고려해야한다고 판단했다.

### 수정 결과

객체 간 커뮤니케이션 체인이 길어지고 날짜계산기가 날짜를 얻어 캘린더를 구성하는 것이 적절하고 날짜계산기로 분리하면 오히려 응집도가 낮아지고 의존도가 높아진다고 판단을 하여 반영하지 않았다.

<hr/>

## Final Sequence Diagram

![class-Page-4 (1)](https://user-images.githubusercontent.com/52988414/118362458-88519000-b5ca-11eb-9042-0e93f67f250c.png)
