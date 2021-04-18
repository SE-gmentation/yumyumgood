# 식당 담당자

---

## 0. 진입 화면

`Initial design`
|UI|Analysis|
|--|--|
| <img src="UI_image/1_1.png" height="300px">|- 현재 시간 판매중인 식사 때가 언제인 지 명시해야함. </br> - 메뉴 관리에서 판매 현황 조회와 메뉴 상태 관리 두 가지 기능을 제공함. </br> 판매 중 빠르게 확인이 가능해야하므로 나누는 것이 적합함.|

`Re-design`

<center>
<img src="UI_image/1_2.png" height="300px">
</center>

## 1. QR코드 인식

`Initial design`
|UI|Analysis|
|--|--|
| <img src="UI_image/2_1.png" height="300px">|- 인식 화면이 디바이스에서 켜져있어야 하므로 화면유지, 터치 제한기능이 필요함 </br> - 가로로 디바이스를 위치해야하는 경우를 고려해 카메라 전환기능이 필요함. </br> - 점원이 직접 코드를 인식하지 않아 인력을 아낄 수 있음.|

`Re-design`

<center>
<img src="UI_image/2_2.png" width="300px">
<img src="UI_image/2_2-1.png" height="300px">
</center>

</br>
</br>

## 2. 메뉴 상태 관리

- 판매 메뉴에 대한 최대 판매 수량(인분) 등록
- 판매 메뉴 비활성화(품절, 판매 중지 등)

`Initial design`
|UI|Analysis|
|--|--|
| <img src="UI_image/4_1.png" height="300px">|- 한 식당에 메뉴마다 판매 시간이 다른 경우가 존재하므로 시간을 메뉴마다 적어야함. </br> - 판매상태, 재고 준비량을 중복해서 적을 필요가 없음. </br> 다른 날짜를 보려면 계속 버튼을 눌러야해서 불편하므로 캘린더로 날짜를 선택할 수 있도록 함.|

`Re-design`

<center>
<img src="UI_image/4_2-2.png" height="300px">
<img src="UI_image/4_2.png" height="300px">
</center>

</br>

## 3. 판매 현황 조회

`Initial design`
|UI|Analysis|
|--|--|
| <img src="UI_image/3_1.png" height="300px">|- 현재 메뉴 주문 내역과 실제 음식 수령 내역을 확인 </br> - 판매 메뉴에 대한 최대 판매 수량 </br> - 주문 현황을 보고 바로 메뉴를 비활성화할 수 있도록 버튼을 추가해야함|

`Redesign`

<center>
<img src="UI_image/3_2.png" height="300px">
</center>

# 전체 학식당 관리자

---
