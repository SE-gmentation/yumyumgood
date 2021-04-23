# Domain Model

> 20193057 김승아, 20190323 배인경

<hr/>

## 목차

#### [1. UC-1 실시간 거래](#UC-1-실시간-거래)

#### [2. UC-2 식당 담당자의 메뉴 관리](#UC-2-식당-담당자의-메뉴-관리)

#### [3. UC-3 거래 자료](#UC-3-거래-자료)

#### [4. UC-4 통계 자료](#UC-4-통계-자료)

#### [5. UC-5 Date Picker](#UC-5-Date-Picker)

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

<hr/>

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

<hr/>

## UC-3 거래 자료

### Extracting the Responsibilities

|                                         Responsibility Description                                          | Type |     Concept Name      |
| :---------------------------------------------------------------------------------------------------------: | :--: | :-------------------: |
|                 UC-3과 관련된 컨셉의 행동들을 조절하고 해당 작업을 다른 컨셉에게 전달한다.                  |  D   |       컨트롤러        |
|                                      로그인 상태를 연장하기 위한 요쳥                                       |  K   | 로그인 상태 연장 요청 |
|                     로그인 상태 요청을 기준으로 30분 간 시간을 측정한다. (UC-3, Step2)                      |  D   |        카운터         |
|                카운터에서 30분이 지나면 자동으로 로그아웃 상태로 업데이트한다. (UC-3, Step2)                |  D   |       로그아웃        |
|                     중앙대 내 학식 전체 관리자가 요청한 조건에 부합하는 모든 거래 내역                      |  K   |  거래 내역 확인 요청  |
|         중앙대 내 학식 전체 관리자가 조건을 선택한다<br/>(거래종류/최신 순/오래된 순) (UC-3, Step5)         |  K   | 조건 데이터 추출 요청 |
|                                  중앙대 내 학식 전체 관리자가 원하는 날짜                                   |  K   |    날짜 선택 요청     |
|                        주문, 주문취소, 판매완료 정보를 얻기 위해 거래 DB를 연결한다.                        |  D   |   거래 관련 DB 연결   |
|                     데이터 베이스로부터 받은 거래 정보를 처리 된 조건 순으로 정렬한다.                      |  D   |      후처리 장치      |
|   중앙대 내 학식 전체 관리자가 선택한 조건들을 고려하여 선택된 데이터를 추출 하여 HTML문서를 렌더링한다.    |  D   |      페이지 생성      |
| 중앙대 내 학식 전체 관리자에게 선택된 조건에 따라 업데이트 된 거래 내역 페이지를 보여준다. (UC-3, Step4, 6) |  D   |      디스플레이       |

### Extracting the Associations

|            Concept Pair            |                                                                Associations description                                                                 |  Association Name   |
| :--------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------: |
|  컨트롤러 <-> 거래 내역 확인 요청  |                       거래 내역 확인 요청이 UI 에 등장하는 ‘거래 트랜젝션 보기' 버튼을 클릭하면 컨트롤러는 해당 신호를 수신한다.                        |        수신         |
|     디스플레이 <-> 페이지 생성     |                                    페이지 생성은 컨트롤러에서 요청받은 것들을 바탕으로 알맞은 디스플레이를 준비한다.                                    |        준비         |
|      컨트롤러 <-> 디스플레이       |                                                 컨트롤러는 페이지 생성이 준비한 디스플레이를 게시한다.                                                  |        게시         |
| 컨트롤러 <-> 로그인 상태 연장 요청 |                           로그인 상태 연장 요청이 UI 에 등장하는 ‘연장하기’ 버튼을 클릭하면 컨트롤러는 해당 신호를 수신한다.                            |        수신         |
|        카운터 <-> 컨트롤러         |                               컨트롤러는 수신 받았던 로그인 연장 신호의 시간을 바탕으로 30분을 다시 측정할 것을 요청한다.                               |        요청         |
|        로그아웃 <-> 카운터         |                                               카운터에서 측정한 시간이 30분이 지나면 로그아웃을 요청한다.                                               |        요청         |
|      디스플레이 <-> 로그아웃       |                                                            로그아웃된 디스플레이를 준비한다.                                                            |        준비         |
| 컨트롤러 <-> 조건 데이터 추출 요청 | 조건 데이터 추출 요청이 UI 에 등장하는 ‘주문’, '주문 취소', '판매완료', '최신 순', '오래된 순' 버튼 중 하나를 클릭하면 컨트롤러는 해당 신호를 수신한다. |        수신         |
|    컨트롤러 <-> 날짜 선택 요청     |                                날짜 선택 요청이 UI 에 등장하는 ‘캘린더' 버튼을 클릭하면 컨트롤러는 해당 신호를 수신한다.                                |        수신         |
|   컨트롤러 <-> 거래관련 DB 연결    |                         컨트롤러는 거래 트랜젝션을 조건에 맞게 가공하기 위해 모든 거래 정보가 저장되어 있는 거래DB와 연결한다.                          |     데이터 제공     |
|      후처리 장치 <-> 컨트롤러      |                                   컨트롤러에 수신 된 조건을 후처리 장치에 보내 필요한 데이터만 추출할 것을 요청한다.                                    |        요청         |
|  후처리 장치 <-> 거래관련 DB 연결  |                                               거래 DB에서 거래 관련 데이터를 모두 후처리 장치로 전달한다.                                               |     데이터 전달     |
|  거래관련 DB 연결 <-> 후처리 장치  |                                                         조건에 맞추어 정렬된 데이터를 전달한다.                                                         | 정렬 된 데이터 전달 |

### Extracting the Attributes

|        Concept        |       Attributes       |                                                         Attribute Description                                                          |
| :-------------------: | :--------------------: | :------------------------------------------------------------------------------------------------------------------------------------: |
| 조건 데이터 추출 요청 |     조건 선택 버튼     |                                         조건 선택 버튼이 있어야 조건 데이터를 추출할 수 있다.                                          |
|    날짜 선택 요청     |      캘린더 버튼       |                                            캘린더 버튼이 있어야 날짜 조건을 선택할 수 있다.                                            |
| 로그인 상태 연장 요청 | (로그인) 연장하기 버튼 |                                      (로그인) 연장하기 버튼이 있어야 자동 로그인을 막을 수 있다.                                       |
|        카운터         |      로그인 시간       | 최초 로그인 시간 또는 연장하기 버튼을 통해 업데이트 된 로그인 시간 정보를 속성값으로 갖고 있어야 30분 뒤에 자동 로그아웃을 할 수 있다. |
|      후처리 장치      |      조건 순 정렬      |                    후처리 장치에서 조건을 수신 받아 조건 순으로 데이터를 정렬하여야 원하는 데이터만 내보낼 수 있다.                    |

### Domain Model for UC-3

![image](https://user-images.githubusercontent.com/65646971/115915432-498a5780-a4ae-11eb-9635-199b0b69cd5d.png)

<hr/>

## UC-4 통계 자료

### Extracting the Responsibilities

|                                                                    Responsibility Description                                                                    | Type |         Concept Name         |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------------: | :--: | :--------------------------: |
|                                            UC-4와 관련된 컨셉의 행동들을 조절하고 해당 작업을 다른 컨셉에게 전달한다.                                            |  D   |           컨트롤러           |
|                                                                 로그인 상태를 연장하기 위한 요쳥                                                                 |  K   |    로그인 상태 연장 요청     |
|                                                로그인 상태 요청을 기준으로 30분 간 시간을 측정한다. (UC-4, Step2)                                                |  D   |            카운터            |
|                                          카운터에서 30분이 지나면 자동으로 로그아웃 상태로 업데이트한다. (UC-4, Step2)                                           |  D   |           로그아웃           |
|                                                          중앙대 내 학식 전체 관리자가 요청한 통계 자료                                                           |  K   |     통계 자료 확인 요청      |
|                                                            냠냠굿 기준 인기 순으로 정렬된 메뉴 리스트                                                            |  K   |    인기 메뉴 리스트 요청     |
|                                                        냠냠굿 기준 수익률 상위 순으로 정렬된 메뉴 리스트                                                         |  K   | 수익률 상위 메뉴 리스트 요청 |
|                                 중앙대 내 학식 전체 관리자가 기간을 선택한다<br/>(1주일/ 1개월/ 3개월/ 6개월/ 1년) (UC-4, Step4)                                 |  K   |        기간 선택 요청        |
|                         중앙대 내 학식 전체 관리자가 인기/수익률 상위 메뉴 선정에 대한 기준을 설명하는 모달창을 팝업한다. (UC-4, Step6)                          |  K   |    냠냠굿 기준 팝업 요청     |
|                                                     실판매량, 남은 재고 정보를 얻기 위해 거래 DB를 연결한다.                                                     |  D   |      거래 관련 DB 연결       |
|                                                            리뷰 평점을 얻기 위해 리뷰 DB를 연결한다.                                                             |  D   |      리뷰 관련 DB 연결       |
| 냠냠굿 기준 인기 알고리즘으로 인기값을 계산하여 도출한 인기 메뉴 리스트를 구한다. <br/>(UC-4, Step3) _(리뷰 평점 + (실판매량 * 0.8 - 남은 재고 * 0.2) \* 0.01 )_ |  D   |        인기 메뉴 계산        |
|      냠냠굿 기준 수익률 알고리즘으로 수익률값을 계산하여 도출한 수익률 상위 메뉴 리스트를 구한다. <br/>(UC-4, Step3) _( 실판매량 * 0.5 - 남은재고 * 0.5 )_       |  D   |    수익률 상위 메뉴 계산     |
|                                           중앙대 내 학식 전체 관리자가 원하는 통계 자료에 대한 HTML문서를 렌더링한다.                                            |  D   |         페이지 생성          |
|                                   거래 정보가 없는 기간의 버튼을 선택하는 오류 발생 시 예외를 알려주는 HTML 문서를 렌더링한다.                                   |  D   |       에러 페이지 생성       |
|                                          중앙대 내 학식 전체 관리자가 원하는 통계 자료 페이지를 보여준다. (UC-4, Step9)                                          |  D   |          디스플레이          |

### Extracting the Associations

|                Concept Pair                |                                                      Associations description                                                      |  Association Name   |
| :----------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------: | :-----------------: |
|      컨트롤러 <-> 통계 자료 확인 요청      |               통계 자료 확인 요청이 UI 에 등장하는 ‘통계 자료 보기' 버튼을 클릭하면 컨트롤러는 해당 신호를 수신한다.               |        수신         |
|         디스플레이 <-> 페이지 생성         |                         페이지 생성은 컨트롤러에서 요청받은 것들을 바탕으로 알맞은 디스플레이를 준비한다.                          |        준비         |
|      디스플레이 <-> 에러 페이지 생성       |                        에러 페이지 생성은 컨트롤러에서 요청받은 것들을 바탕으로 에러 디스플레이를 준비한다.                        |        준비         |
|          컨트롤러 <-> 디스플레이           |                                 컨트롤러는 페이지/에러 페이지 생성이 준비한 디스플레이를 게시한다.                                 |        게시         |
|     컨트롤러 <-> 로그인 상태 연장 요청     |                 로그인 상태 연장 요청이 UI 에 등장하는 ‘연장하기’ 버튼을 클릭하면 컨트롤러는 해당 신호를 수신한다.                 |        수신         |
|            카운터 <-> 컨트롤러             |                    컨트롤러는 수신 받았던 로그인 연장 신호의 시간을 바탕으로 30분을 다시 측정할 것을 요청한다.                     |        요청         |
|            로그아웃 <-> 카운터             |                                    카운터에서 측정한 시간이 30분이 지나면 로그아웃을 요청한다.                                     |        요청         |
|          디스플레이 <-> 로그아웃           |                                                 로그아웃된 디스플레이를 준비한다.                                                  |        준비         |
|     컨트롤러 <-> 인기 메뉴 리스트 요청     |        인기 메뉴 리스트 요청이 UI 에 등장하는 인기 상위 메뉴 탭의 ‘더보기' 버튼을 클릭하면 컨트롤러는 해당 신호를 수신한다.        |        수신         |
| 컨트롤러 <-> 수익률 상위 메뉴 리스트 요청  |   수익률 상위 메뉴 리스트 요청이 UI 에 등장하는 수익률 상위 메뉴 탭의 ‘더보기' 버튼을 클릭하면 컨트롤러는 해당 신호를 수신한다.    |        수신         |
|        컨트롤러 <-> 기간 선택 요청         | 기간 선택 요청이 UI 에 등장하는 ‘1주일', '1개월', '3개월', '6개월', '1년' 버튼 중 하나를 클릭하면 컨트롤러는 해당 신호를 수신한다. |        수신         |
|     컨트롤러 <-> 냠냠굿 기준 팝업 요청     |               냠냠굿 기준 팝업 요청이 UI 에 등장하는 ‘냠냠굿 기준' 버튼을 클릭하면 컨트롤러는 해당 신호를 수신한다.                |        수신         |
|       컨트롤러 <-> 거래관련 DB 연결        |                       컨트롤러는 통계 자료를 산출하기 위해 모든 거래 정보가 저장되어 있는 거래DB와 연결한다.                       |     데이터 제공     |
|        인기 메뉴 계산 <-> 컨트롤러         |               컨트롤러에 수신 된 기간을 인기 메뉴 계산에 조건으로 사용하여 인기 메뉴 리스트를 추출할 것을 요청한다.                |        요청         |
|     수익률 상위 메뉴 계산 <-> 컨트롤러     |        컨트롤러에 수신 된 기간을 수익률 상위 메뉴 계산에 조건으로 사용하여 수익률 상위 메뉴 리스트를 추출할 것을 요청한다.         |        요청         |
|    인기 메뉴 계산 <-> 거래관련 DB 연결     |                                  거래 DB에서 거래 관련 데이터를 모두 인기 메뉴 계산으로 전달한다.                                  |     데이터 전달     |
|    인기 메뉴 계산 <-> 리뷰관련 DB 연결     |                                  리뷰 DB에서 리뷰 평점 데이터를 모두 인기 메뉴 계산으로 전달한다.                                  |     데이터 전달     |
|    거래관련 DB 연결 <-> 인기 메뉴 계산     |                             선택된 기간 동안의 거래와 리뷰 정보로 계산된 인기 메뉴 리스트를 전달한다.                              | 정렬 된 데이터 전달 |
| 수익률 상위 메뉴 계산 <-> 거래관련 DB 연결 |                              거래 DB에서 거래 관련 데이터를 모두 수익률 상위 메뉴 계산으로 전달한다.                               |     데이터 전달     |
| 거래관련 DB 연결 <-> 수익률 상위 메뉴 계산 |                             선택된 기간 동안의 거래 정보로 계산된 수익률 상위 메뉴 리스트를 전달한다.                              | 정렬 된 데이터 전달 |

### Extracting the Attributes

|        Concept        |       Attributes       |                                                         Attribute Description                                                          |
| :-------------------: | :--------------------: | :------------------------------------------------------------------------------------------------------------------------------------: |
|    기간 선택 요청     |       기간 버튼        |                                             기간 버튼이 있어야 통계 기간을 설정할 수 있다.                                             |
| 냠냠굿 기준 팝업 요청 |    냠냠굿 기준 버튼    |                                냠냠굿 기준 버튼이 있어야 냠냠굿 기준을 설명할 모달창을 팝업할 수 있다.                                 |
| 로그인 상태 연장 요청 | (로그인) 연장하기 버튼 |                                      (로그인) 연장하기 버튼이 있어야 자동 로그인을 막을 수 있다.                                       |
|        카운터         |      로그인 시간       | 최초 로그인 시간 또는 연장하기 버튼을 통해 업데이트 된 로그인 시간 정보를 속성값으로 갖고 있어야 30분 뒤에 자동 로그아웃을 할 수 있다. |
|    인기 메뉴 계산     |   냠냠굿 기준 인기값   |                              냠냠굿 기준으로 계산한 인기값을 반환하며 인기 순으로 메뉴 리스트를 전달한다.                              |
| 수익률 상위 메뉴 계산 |  냠냠굿 기준 수익률값  |                         냠냠굿 기준으로 계산한 수익률값을 반환하며 수익률 상위 순으로 메뉴 리스트를 전달한다.                          |

### Domain Model for UC-4

![image](https://user-images.githubusercontent.com/65646971/115926099-3632b880-a4bd-11eb-8b7a-76410c62ca27.png)

<hr/>

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
