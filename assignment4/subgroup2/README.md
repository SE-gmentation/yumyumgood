## ✨ Github Link

- https://github.com/SE-gmentation/yumyumgood_subgroup2

## 📢 SubGroup 2

- 주제 소개 
  - 전체/학식당 관리자의 메뉴 관리 및 통계 서비스를 맡은 SUBGROUP2 김승아/배인경 입니다.
  - 총 5가지의 USE-CASE 중 학식당 담당 관리자와 관련된 UC-2, UC-5의 기능을 구현했습니다.
  - UC2 : 식당 담당자의 메뉴 관리
  - UC5 : Date Picker

- 기능 명세
  - 학식당 담당 관리자 인터페이스 페이지 구현
  - 접속한 학식당 담당 관리자에 따른 DB 조회
  - 날짜별 학식당의 조/중/석식 메뉴 조회
  - 캘린더를 통한 조회 날짜 변경과 DB 연결
  - 메뉴 판매상태 및 재고 관리

<br/>

## 🔨 Tech stacks & Language

- Python3
- Django
- sqlite
- HTML
- CSS
- JS
- Bootstrap

<br/>

## 🔎 Getting Started
1. Clone this repository

   ```bash
   $ git clone https://github.com/SE-gmentation/yumyumgood_subgroup2.git
   ```

2. 가상환경(venv) 설치 

   ```bash
   $ python -m venv venv 
   ```

3. 가상환경(venv) 실행

   ```bash
   $ source venv\Scripts\activate
   ```
   
4. Install Requirements for project

   ```bash
   $ pip install -r requirements.txt 
   ```
   
5. Migration for DB (Command execution location must be where manage.py is located.) 

   ```bash
   $ python manage.py makemigrations
   $ python manage.py migrate
   ```
   
6. Create Superuser for Admin -> Set Username & Password (Command execution location must be where manage.py is located.) 

   ```bash
   $ python manage.py createsuperuser
   ```
   
7. Run (Command execution location must be where manage.py is located.) 

   ```bash
   $ python manage.py runserver
   ```

> DB 내용(Profile(User), Menu, Cafeteria)은 서버가 실행 된 로컬에서 http://127.0.0.1:8000/admin/ 사이트를 통해 일괄적으로 작성 및 관리하여 데모를 진행했습니다. 관련하여 궁금하신 점은 Issues 부탁드립니다.

<br/>

## 📸 Features & Demo Screenshot

- **DB구축**
  - UC-2, UC-5 구현을 위한 DB 설계

  - ERD  
  <img src="https://user-images.githubusercontent.com/52988414/119694819-8d46f700-be88-11eb-97ad-f872866d3c4b.png" height=400 />

  - sqlite 적용  
  <img src="https://user-images.githubusercontent.com/52988414/120183484-b67dd380-c24a-11eb-8aaf-caece689e776.png" height=600/>

- **웹앱으로 페이지 구성**
  - 모바일 화면 크기로 웹페이지를 구성
  
    <img src="https://user-images.githubusercontent.com/52988414/120182754-c34df780-c249-11eb-9d18-8418a8bcbc8f.png" height="300"/>
    <img src="https://user-images.githubusercontent.com/52988414/120183627-e75e0880-c24a-11eb-8df8-c2d50fa1131c.png" height="300"/>

- **( UC-2 )  담당자 식당 별 인터페이스 페이지**
  - 접속한 user의 cafeteria storage를 조회하여 인터페이스 페이지를 구성한다.
  <p align="center">
  <img src="https://user-images.githubusercontent.com/52988414/120185111-bf6fa480-c24c-11eb-8b75-0ca1f3f9bdde.png" width=300/>
  </p>
  
- **( UC-2 )  메뉴 상태 관리**
  - 식당 정보화 date storage를 통해 오늘 날짜에 해당하는 조회 쿼리를 보내 Menu를 DB에서 불러옴.
  - 날짜 정보는 url parameter로 전송함.  
  <img src="https://user-images.githubusercontent.com/52988414/120187181-71a86b80-c24f-11eb-887c-e052d9885c6a.png" height=25/>

  - Menu 정보로 html 페이지를 렌더링함.
  <p align="center">
  <img src="https://user-images.githubusercontent.com/52988414/120186224-2e013200-c24e-11eb-9749-9108c1e1caef.png" width=300/>
  </p>

- **( UC-5 ) 캘린더 모달**
  - 캘린더 버튼을 선택하면 Modal html을 렌더링하여 모달을 팝업
  - date storage 기준으로 캘린더 모달 구성
  
  <p align="center">
  <img src="https://user-images.githubusercontent.com/52988414/120187405-b3391680-c24f-11eb-9aa4-ef8e16a97c22.png" width=300/>
  </p>

- **( UC-2 ) 메뉴 정보 수정**

  - 정보 수정 버튼을 선택하여 해당 날짜의 판매 메뉴 정보 수정
  - 판매상태, 재고 레이블을 텍스트 박스로 바꾸어 수정할 수 있도록 함
  - 저장하기 버튼을 선택하면 변경된 정보로 DB를 업데이트함.

  <p align="center">
  <img src="https://user-images.githubusercontent.com/52988414/120188028-8e916e80-c250-11eb-8d9b-8e5fee4aa4ed.png" width=300/>
  </p>
  
<br/>

## 📍 SSD(Class Diagram) 대조표

>   | SSD 내 컨셉(클래스)이름 | 클래스명(함수명) |
>   | --- | ---  |
>   |**class Date Converter** : YYYY-MM-dd 형태로 url의 param으로 Date를 받음 |Date Accessor(Date Storage 객체)|
>   |**profile = Profile.objects.get(user = request.user)** : sqlite에서 현재 접속한 User에 대한 정보를 조회|User DB Accessor|
>   |**menus = Menu.objects.filter(sale_date = date, cafeteria = profile.Cafeteria)** : sqlite에서 현재 접속한 user의 식당인 지, 판매 날짜가 일치하는 지 확인한 메뉴 데이터를 조회 |Menu DB Accessor|
>   |**return render(request,'manager/initialpage.html', data)** |interfacePage := render(menuList)|
>   |**return render(request,'manager/manage_read.html', data)** |savePage := saveRender()|
>   |**return render(request,'manager/manage_update.html', data)** |editPage := renderEdit()|
>   |**def menu_edit(request, date)** |updateStatus(status)|
>   |**status=request.POST.get('status['+str(i)+']')**<br>**quantity=request.POST.get('quantity['+str(i)+']')**<br>#DB에 바꿀 내용들<br>**changeMenu.status=status**<br>**changeMenu.quantity=quantity**|setStatus, setAmount|
>   |**def menu_update(request, date)**|edit(), save()|
>   |views.py|Controller|
>   |**date**|today|
>   |**target**|target|
>   |**changeDate, changeMonth, changeYear**|Date calculator의 함수|
>   |**place()**|makeCalendar|
>   |**getDate()**|getDay|
>   |**DatePicker**|Interface Button|
>   |**moveDay, moveMonth, moveYear**|checkButton|

<br/>

## 💻 참고사항
- 코드작업은 organization 내 yumyumgood_subgroup2에서 진행 했습니다.
- DB 내용(Profile(User), Menu, Cafeteria)은 서버가 실행 된 로컬에서 http://127.0.0.1:8000/admin/ 사이트를 통해 일괄적으로 작성 및 관리하여 데모를 진행했습니다. 관련하여 궁금하신 점은 Issues 부탁드립니다.
- Subgroup2는 Github의 Issues를 적극 활용하여 구현(개발)을 진행했습니다.
<p align="center">
<img src="https://user-images.githubusercontent.com/52988414/120179634-cf37ba80-c245-11eb-9ed9-c7c713337a43.png" width=600/>
</p>



