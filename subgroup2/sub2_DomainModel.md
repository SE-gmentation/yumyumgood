# Domain Model

> 20193057 김승아, 20190323 배인경

<hr/>

## 목차

#### [1. UC-1 실시간 거래](#UC-1-실시간-거래)

#### [2. UC-2 식당 담당자의 메뉴 관리](#UC-2-식당-담당자의-메뉴-관리)

#### [2. UC-3 거래 자료](#UC-3-거래-자료)

#### [2. UC-4 통계 자료](#UC-4-통계-자료)

#### [2. UC-5 Date Picker](#UC-5-Date-Picker)

<hr/>

## UC-1 실시간 거래

### Extracting the Responsibilities

|                             Responsibility Description                             | Type |  Concept Name  |
| :--------------------------------------------------------------------------------: | :--: | :------------: |
|             전체 시스템과 관련된 모든 컨셉의 작업을 조정하고 지시한다.             |  D   |   Controller   |
|  Actor가 속한 식당, 현재 식사 시간, 수행할 수 있는 작업 버튼을 보여주는 HTML 문서  |  K   | Interface Page |
|           QR코드가 카메라의 사각테두리 안에 인식되면 이미지로 캡쳐한다.            |  D   |   QRCatcher    |
|   QR 코드에서 추출한 주문 정보와 인증 정보(주문번호, 주문한 메뉴, 주문 시간 등)    |  K   |     Order      |
| 스캐너 사용 중 디바이스를 잠금모드로 설정하여 터치, 뒤뢰가기 등의 작용을 무시한다. |  D   | Scanner Locker |
|                카메라를 90도 회전하여 스캐너를 가로모드로 전환한다.                |  D   | Scanner Turner |
|                    스캐너에 인식된 QR코드가 유효한 지 확인한다.                    |  D   |   QRChecker    |
|                          주문 정보를 읽는 알람을 울린다.                           |  D   | AlarmOperator  |
|                              실시간 거래 정보 보관소                               |  K   |   PayStorage   |
|                       누적된 거래 정보를 저장소에 기록한다.                        |  D   |     Logger     |

- QR코드 자체에 유효한 지 판단할 수 있는 정보가 내재되어 있으므로 Storage는 필요하지 않음.

### Extracting the Associations

|          Concept Pair          |                         Associations description                          | Association Name  |
| :----------------------------: | :-----------------------------------------------------------------------: | :---------------: |
|  InterfacePage <-> Controller  |    InterfacePage는 Controller에 QRScanner 및 Scanner 조절을 요청한다.     |     requests      |
| ScannerAdjuster <-> Controller |   Controller는 ScannerAdjuster에게 lock/Dispalay Mode 변경을 요청한다.    |     requests      |
|    QRCatcher <-> Controller    |  QRCatcher는 Controller에게 요청을 전송하고 인식한 QR이미지를 전달한다.   | conveys-requests  |
|    QRChecker <-> Controller    | Controller는 QRChecker에게 인식한 이미지를 전달하고 인증 확인을 요청한다. | conveys-requests  |
|    QRChecker <-> PayStorage    |  QRChecker는 PayStorage에서 결제정보를 조회하고 주문상태를 업데이트한다.  | retreives updates |
|     Logger <-> PayStorage      |             PayStorage는 Logger에게 거래정보 저장을 요청한다.             |   requests save   |
|      QRChecker <-> Order       |                       QRChecker는 Order를 인증한다.                       |     verifies      |
|      Controller <-> Order      |                    Controller는 인증된 Order를 얻는다.                    |      obtains      |
|  AlarmOperator <-> Controller  |            Controller는 Order을 전달하고 알람 작동을 요청한다.            | conveys-requests  |

### Extracting the Attributes

<table>
  <tr>
    <td>Concept</td>
    <td>Attributes</td>
    <td>Description</td>
  </tr>
  <tr>
    <td rowspan="2">interfacePage</td>
    <td>mealTime</td>
    <td>조식, 중식, 석식 중현재 식사시간을 표시</td>
  </tr>
  <tr>
    <td>restaurantData</td>
    <td>접속한 담당자의 식당 정보</td>
  </tr>
    <tr>
    <td rowspan="2">ScannerAdjuster</td>
    <td>lockMode</td>
    <td>잠금 상태(1:True, 0:False)</td>
  </tr>
  <tr>
    <td>DisplayMode</td>
    <td>스캐너 회전 상태(1:세로, 0:가로)</td>
  </tr>
      <tr>
    <td rowspan="4">PayStorage</td>
    <td>payNumber</td>
    <td>결제 번호</td>
  </tr>
  <tr>
    <td>payTime</td>
    <td>결제 시간</td>
  </tr>
  <tr>
    <td>isOrder</td>
    <td>주문/수령 여부</td>
  </tr>
  <tr>
    <td>menu</td>
    <td>메뉴 정보(메뉴 이름, 개수 등)</td>
  </tr>
    <tr>
    <td rowspan="3">Order</td>
    <td>orderNumber</td>
    <td>주문 번호</td>
  </tr>
  <tr>
    <td>orderTime</td>
    <td>주문 시간</td>
  </tr>
  <tr>
    <td>menu</td>
    <td>메뉴 정보(메뉴 이름, 개수 등)</td>
  </tr>
</table>

### Domain Model for UC-1

![UC-1](https://user-images.githubusercontent.com/52988414/115936849-510f2800-a4d1-11eb-841b-b7d5ee80e053.png)

## UC-2 식당 담당자의 메뉴 관리

### Extracting the Responsibilities

|                            Responsibility Description                            | Type |    Concept Name     |
| :------------------------------------------------------------------------------: | :--: | :-----------------: |
|            전체 시스템과 관련된 모든 컨셉의 작업을 조정하고 지시한다.            |  D   |     Controller      |
| Actor가 속한 식당, 현재 식사 시간, 수행할 수 있는 작업 버튼을 보여주는 HTML 문서 |  K   |   Interface Page    |
|              데이터베이스 로그 검색을 위한 날짜 값 (기본 값은 오늘)              |  K   |    Date Request     |
|   Actor가 선택한 날짜에 대한 데이터베이스 질의문을 준비하고 레코드를 조회한다.   |  D   | Database Connection |
|            검색된 레코드를 HTML 문서로 렌더링하여 Actor에게 전송한다.            |  D   |      PageMaker      |
| 준비된 재고가 소진되는 지(재고수량 - 결제수량 = 0) 판단하고 판매상태를 변경한다. |  D   |    SalesChanger     |

### Extracting the Associations

|           Concept Pair            |                                   Associations description                                   | Association Name |
| :-------------------------------: | :------------------------------------------------------------------------------------------: | :--------------: |
|    Controller <-> DateRequest     |                       Controller는 DateRequest로부터 날짜 값을 받는다.                       |     receives     |
|  SalesManager <-> InterfacePage   |               SalesManager는 InterfacePage로부터 각 메뉴에 관한 정보를 받는다.               |     receives     |
|    Controller <-> SalesManager    | SalesManager는 Controller에게 요청을 전송하고 판매 상태를 관리해야하는 메뉴 정보를 전달한다. | conveys requests |
|   Controller <-> InterfacePage    |               Controller는 InterfacePage에 필터랑하여 조회한 레코드를 보낸다.                |      posts       |
|    PageMaker <-> InterfacePage    |                           Page Maker는 Interface Page를 준비한다.                            |     prepares     |
|     Controller <-> PageMaker      |          Controller는 Page Maker에게 요청을 전송하고 표시가 준비된 페이지를 받는다.          | conveys requests |
| PageMaker <-> DatebaseConnection  |   Database Connection은 조회한 데이터를 렌더링하여 표시하기 위해 Page Maker에게 전달한다.    |  provides data   |
| Controller <-> DatebaseConnection |                  Controller는 Database Connection에게 검색 요청을 전송한다.                  | conveys requests |

### Extracting the Attributes

<table>
  <tr>
    <td>Concept</td>
    <td>Attributes</td>
    <td>Description</td>
  </tr>
    <tr>
    <td rowspan="3">InterfacePage</td>
    <td>menuData</td>
    <td>메뉴 정보</td>
  </tr>
  <tr>
    <td>salesStatus</td>
    <td>판매 상태</td>
  </tr>
  <tr>
    <td>maxNumOfSales</td>
    <td>판매 가능 수량, 재고 준비량</td>
  </tr>
      <tr>
    <td >DateRequest</td>
    <td>searchDate</td>
    <td>조회 날짜</td>
  </tr>
  <tr>
    <td >SalesManager</td>
    <td>numOfSales</td>
    <td>실시간 결제 수량</td>
  </tr>
</table>

### Domain Model for UC-2

![UC-2](https://user-images.githubusercontent.com/52988414/115936852-53718200-a4d1-11eb-8f29-5abb942e02b6.png)

## UC-3 거래 자료

### Extracting the Responsibilities

| Responsibility Description | Type | Concept Name |
| :------------------------: | :--: | :----------: |

### Extracting the Associations

| Concept Pair | Associations description | Association Name |
| :----------: | :----------------------: | :--------------: |

### Extracting the Attributes

| Concept | Attributes | Attribute Description |
| :-----: | :--------: | :-------------------: |

### Domain Model for UC-3

###

## UC-4 통계 자료

## UC-5 Date Picker

### Extracting the Responsibilities

|                          Responsibility Description                          | Type |    Concept Name     |
| :--------------------------------------------------------------------------: | :--: | :-----------------: |
|          전체 시스템과 관련된 모든 컨셉의 작업을 조정하고 지시한다.          |  D   |     Controller      |
|               캘린더에 올바른 날짜 정보를 보여주는 모달창 양식               |  K   |   Interface Page    |
|                         캘린더를 페이지에 출력한다.                          |  D   |    CalendarMaker    |
| Actor가 선택한 날짜에 대한 데이터베이스 질의문을 준비하고 레코드를 조회한다. |  D   | Database Connection |

### Extracting the Associations

|             Concept Pair             |                                  Associations description                                  | Association Name |
| :----------------------------------: | :----------------------------------------------------------------------------------------: | :--------------: |
|     InterfacePage <-> Controller     |                     Controller는 InterfacePage로부터 날짜 값을 받는다.                     |     receives     |
|     InterfacePage <-> Controller     |             Controller는 InterfacePage에게 필터랑하여 조회한 레코드를 보낸다.              |      posts       |
|   InterfacePage <-> CalendarMaker    |                         CalendarMaker는 Interface Page를 준비한다.                         |     prepares     |
|     Controller <-> CalendarMaker     |       Controller는 CalendarMaker에게 요청을 전송하고 표시가 준비된 페이지를 받는다.        | conveys requests |
| CalendarMaker <-> DatebaseConnection | Database Connection은 조회한 데이터를 렌더링하여 표시하기 위해 CalendarMaker에게 전달한다. |  provides data   |

### Extracting the Attributes

|    Concept    |  Attributes  | Attribute Description |
| :-----------: | :----------: | :-------------------: |
| InterfacePage | selectedDate |  현재 선택된 날짜 값  |

### Domain Model for UC-5

![UC-5](https://user-images.githubusercontent.com/52988414/115938638-6175d180-a4d6-11eb-9a9a-58c08a22b2c3.png)
