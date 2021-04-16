# Gathered Requirements 2

## Requirements analysis -> Functional/Nonfunctional/User-Interface

> 20193057 김승아, 20190323 배인경

<hr/>

### 1. Functional Requirements
- 이 시스템은 Socket 통신을 통해 실시간으로 결제 및 결제 취소 확인을 하고 주문 내역을 수정한다.
- 각 식당 담당자는 식당 이용자들의 QR코드를 인식하여 실 판매 수량을 관리한다.
- 각 식당 담당자는 판매중인 메뉴를 현장 상황에 따라 유연하게 비활성화하여 메뉴 판매 중지를 시키고 유연하게 재활성화하여 다시 판매할 수 있다.
- 중앙대 내 학식 전체 관리자는 날짜 범위, 각 학식당 별, 판매수량, 남은 음식량, 수익성, 리뷰 평점 순 등 여러 조건을 선택하여 트랜잭션을 확인할 수 있다.

### 2. Non-Functional Requirements
> FURPS + (Functionality, Usability, Reliability, Performance, Supportability)

1. F (Functionality)(Security)
- 서버 관리자는 중앙대 내 학식 전체 관리자가 아닌 사람들은 트랜젝션을 확인할 수 없도록 트랜잭션 정보(DB) 보호에 유념해야 한다.

- 각 식당 담당자별로 확인할 수 있는 현재 메뉴 주문 내역과 실제 음식 수령 내역이 다르므로 해당 정보 외에는 알 수 없도록 정보(DB) 보호에 유념해야한다.

- 중앙대 포탈에서 학식 메뉴 목록을 크롤링을 통해 가져오므로 중앙대 포탈 서버가 다운될 때를 대비하여야 한다.
> 기존에 중앙대 포탈의 '주간 식단'에 매주 일주일 치 식단이 각 학식당 별로 업데이트 된다.

2. U (Usability)

- 이 서비스의 고객층은 중앙대 내 학식 전체 관리자, 각 식당 담당자, 식당 이용자인가에 따라 필요한 기능이 다르므로 UI가 달라야 한다.

- UX Writing에 있어서 사용자의 말로 간결하고도 유용한 언어를 사용하도록 UI를 구성하여 서비스 사용자(페르소나)의 입장에서 서비스를 사용하는 데 거부감이 없도록 해야한다.

3. R (Reliability)

- 학식 관리자와 이용자의 주문 내역 및 서비스 권한의 안정성을 보장하기 위한 대응책을 마련해야 한다.

4. P (Performance)

- 중앙대 포탈의 '주간 식단'의 메뉴와 본 서비스의 학식 메뉴가 다른 혼동이 발생되지 않아야 한다.

5. S (Supportability)

- 사용자 트래픽이 급증할 경우에 서버가 꺼지지 않도록 대응책을 마련해야 한다.

### 3. User-Interface Requirements




_To-do_

1. User Interface 방식으로 requirements 작성하기
> 각 식당 담당자, 중앙대 내 학식 전체 관리자의 입장에 따라 다른 UI 구성

2. Analysis를 바탕으로 Refined User Story 작성 -> new file
> Identifier 이름을 ST로 바꾸고 합쳐져야하거나 분리시켜야하는 요구사항들 생각해보기






