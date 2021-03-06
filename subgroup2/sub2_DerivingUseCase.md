# 목차

### [1. From System Requirements](#From-System-Requirements)

### [2. Use Case Diagram](#Use-Case-Diagram)

### [3. Traceability Matrix](#Traceability-Matrix)

---

## From System Requirements

| Actor                      | Actor's Goal                                                                                                 | Use Case                         |
| -------------------------- | ------------------------------------------------------------------------------------------------------------ | -------------------------------- |
| 식당 담당자                | 그 날의 판매 메뉴에 대한 최대 판매 수량(인분)을 영업 전에 미리 등록하기 위함.                                | 식당담당자의 메뉴관리 (UC-2)     |
| QR코드 스캐너              | 식당 이용자가 제시한 QR코드를 인식하기 위함.                                                                 | 실시간 거래 (UC-1)               |
| QR코드 스캐너              | 정확한 주문량 판단을 위해 결제가 취소된 경우 주문 내역을 즉시 수정하기 위함.                               | 실시간 거래 (UC-1)               |
| 식당 담당자                | 식당 이용자가 제시한 QR코드를 인식한 후 음식을 식당 이용자에게 제공하여 실 판매 수량(인분)을 관리하기 위함. | 실시간 거래 (UC-1)               |
| 식당 담당자                | 판매중인 메뉴를 비활성화하여 메뉴 판매를 중지시키기 위함.                                                   | 식당담당자의 메뉴관리 (UC-2)     |
| 식당 담당자                | 현재 메뉴 주문 내역과 실제 음식 수령 내역을 확인하기 위함.                                                  | 실시간 거래 (UC-1), 거래 자료 (UC-3) |
| 중앙대 내 학식 전체 관리자 | 중앙대 내 전체 학식당의 학식 거래에 관한 거래 트랜젝션 보기, 통계 자료 보기, 리뷰 관리를 하기 위함.         | 거래 자료(UC-3), 통계 자료(UC-4) |
| 중앙대 내 학식 전체 관리자 | 거래종류와 최신 순/오래된 순에 따라 거래 트랜 젝션 정보를 재정렬하기 위함.                                   | 거래 자료(UC-3)                  |
| 중앙대 내 학식 전체 관리자 | 모든 건물의 각 학식당 별 학식 거래에 관한 인기 상위 메뉴와 수익률 상위 메뉴를 확인하기 위함.                | 통계 자료(UC-4)                  |
| 중앙대 내 학식 전체 관리자 | 인기 상위 메뉴와 수익률 상위 메뉴 선정에 대한 냠냠굿의 기준을 확인하기 위함.                                | 통계 자료(UC-4)                  |
| 캘린더 버튼                | 빠른 날짜 선택을 위한 캘린더 UI 팝업을 위함.                                                                | UC–2, UC-3                       |
| 연장하기 버튼              | 자동로그인 방지 및 데이터 보안을 위해 로그인 상태 유지 시간을 제한하고 이를 연장하기 위함.                   | UC-3, UC-4                       |

</br>

## Use Case Diagram

![image](https://user-images.githubusercontent.com/65646971/115902459-6c604000-a49d-11eb-8e0d-fcfb4fedd8b8.png)


</br>

## Traceability Matrix

[Refined User Story](https://github.com/SE-gmentation/yumyumgood/blob/main/subgroup2/sub2_RefinedUserStory.md)의 REQ 참고

![image](https://user-images.githubusercontent.com/65646971/115903670-d1686580-a49e-11eb-801a-36beaffee96b.png)

