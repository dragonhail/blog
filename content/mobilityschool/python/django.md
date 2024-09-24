---
title: Django에서의 데이터베이스 연동
linkTitle: Django
weight: 12
---

### Model
- 데이터 서비스를 제공하는 레이어
- 애플리케이션안에 자동으로 생성되는 models.py 파일에 정의
- 클래스 단위로 정의를 하는데 하나의 클래스는 하나의 테이블과 매팽됨
- 모델 클래스를 만들때는 Model 이라는 클래스로부터 상속을 받아야 함
- Primary Key를 설정하지 않으면 테이블을 생성할 때 자동으로 id가 생성됨
- 속성을 생성하면 테이블의 컬럼이 만들어지는데 models에 있는 여러 종류의 클래스를 이용하고 각 클래스마다 생성을 할 때 여러 옵션을 설정하는 것이 가능
- 대다수의 ORM은 테이블이 존재하지 않으면 테이블을 자동으로 생성해주고 제약 조건은 속성의 자료형에 해당하는 클래스에서 생성자나 메서드를 통해서 지정이 가능

### mariadb나 mysql 사용을 위한 설정
- mysqlclient라는 패키지가 필요
- settings.py 파일의 DATABASE 설정 부분을 수정
```python
DATABASES = {
  'default':{
    'ENGINE':'django.db.backends.mysql',
    'NAME':'데이터베이스이름',
    'USER':'계정',
    'PASSWORD':'비밀번호',
    'HOST':'데이터베이스URL',
    'PORT':'포트번호인데 기본 포트를 사용하는 경우 빈 칸으로 설정 가능'
  }
}
```
- 데이터베이스 정보를 수정한 경우는 2개의 명령어를 재실행
- `python manage.py makemigrations`
- `python manage.py migrate`
- models.py 파일에 테이블과 매핑될 클래스를 생성
```python
class Item(models.Model):
  itemid = models.IntegerField(primary_key=True)
  itemname = models.CharField(max_length=20)
  price = models.IntegerField()
  description = models.CharField(max_length=50)
  pictureurl = models.CharField(max_length=20)
```

### CRUD 작업
- 데이터 삽입: 인스턴스를 만들고 save 메서드 호출
- 데이터 조회
  - Model클래스에는 objects라는 Manager 클래스의 인스턴스가 존재
  - objects라는 인스턴스를 통해서 필터링 및 정렬 등의 작업을 수행
  - item테이블의 모든 데이터를 조회: `Item.objects.all()`을 호출하면 반복 가능한 컬렉션으로 데이터를 리턴
  - get, filter, exclude, count, order_by, distinct, first, last와 같은 여러 메서드가 존재
- 데이터 수정
  - 데이터를 조회한 후 필요한 속성의 값을 수정하고 save를 호출하면 됨
- 데이터 삭제
  - 데이터를 조회한 후 delete를 호출하면 됨
- Item 테이블의 전체 데이터를 조회
- views.py 파일의 index 함수를 수정
```python
from myweb.models import Item

# Create your views here.
def index(request):
    # Item테이블의 모든 데이터를 가져오기
    data = Item.objects.all()
    
    return render(request, 'index.html',  {'data': data})
```
- 템플릿 엔진을 사용해서 정적 파일(HTML, CSS, JavaScript, HTML을 출력하기 위해서  필요한 파일들)을 사용할 때는 별도의 설정을 추가: settings.py 파일에 정적 파일의 디렉터리 설정 코드를 추가
```python
# 정적 파일을 저장할 디렉터리 설정
STATICFILES_DIRS = (os.path.join(BASE_DIR, 'static'),)
```
- myweb 디렉터리 안에 static 디렉터리를 생성하고 그 안에 css 디렉터리를 생성하고 style.css 파일을 생성하고 작성
```css
div.body {
    margin-top: 50psx;
    margin-bottom: 50px;
}

tr.header {
    background: #C9BFED;

}

tr.record {
    background: #EDEDED
}
```
- index.html 파일 수정
```python
<% load static %>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>목록</title>
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
    <h3>{{message}}</h3>
</body>
</html>
```
- itemid를 url에서 넘겨받아 하나의 데이터가져오기
  - urls.py 파일에 요청을 추가 
  - `path('detail/<int:itemid>', views.detail),`
- views.py 파일에 detail 함수 추가
```python
def detail(request, itemid):
    # itemid의 값이 itemid인 데이터 1개 가져오기
    item = Item.objects.get(itemid=itemid)
    return HttpResponse(item)
```
- API 테스트 도구를 가지고 detail/존재하는id
- 데이터 삽입 구현
  - urls.py 파일에 삽입을 위한 요청을 생성
  - `path('item', views.insert),`
```python
from django.db.models import Max
from django.shortcuts import redirect

def insert(request):
    item = Item()
    # 가장 큰 itemid를 찾아서 +1을 해서 새로운 itemid 생성
    obj = Item.objects.aggregate(itemid=Max("itemid"))
    if obj['itemid'] == None:
        obj['itemid'] = 0
    item.itemid = int(obj['itemid']) + 1
    item.description = "description"
    item.price = 3000
    item.pictureurl = "image"
    item.itemname = "무화과"
    item.save()

    # 시작 페이지로 리다이렉트
    return redirect("/")
```
- SPA(Single Page Application - 하나의 페이지에서 모든 작업을 수행하는 애플리케이션: angular, vue, react가 SPA를 구현하는  프레임워크)가 아닌 경우 페이지 이동 방법
  - forwarding: 조회에 주로 이용
    - 이전 흐름을 유지하면서 이동
    - request객체가 다시 생성되지 않고 이전 객체를 계속 유지
    - 새로고침을 하게 되면 요청 처리 메서드가 다시 호출됨
  - redirect: 조회 이외의 작업에 주로 이용
    - 이전 흐름을 유지하지 않고 이동
    - request 객체는 다시 생성되고 session 객체는 유지
    - 새로고침을 하게 되면 요청 처리 메서드는 호출되지 않고 결과만 다시 보여짐

## REST API
### API(Application Programming Interface)
- 프로그램과 프로그램을 연결시켜주는 매개체
- 프로그램과 통신을 위해서 제공
- 프레임워크 형태로 제공하기도 하고 데이터 형태로 제공하기도 함
- 비슷한 말로 Software Developer Kit 이라고 하기도 함
- Open API 라고 부르면 API를 누구나 사용할 수 있도록 해준 것

### CSR(Client Side Rendering)
- API Server를 만들어서 데이터를 제공하도록 만들고 클라이언트에서 이 데이터를 제공받아서 출력하는 방식
- Server Side Rendering은 서버가 처리를 한 후 그 데이터를 가지고 템플릿 엔진을 이용해서 HTML을 만들어서 클라이언트에게 제공하는 방식
- CSR 방식은 클라이언트에서 데이터를 가공해서 화면에 출력을 하기 때문에 데이터를 어떤 형식으로 주고 받을지 결정을 해야 하는데 가장 많이 사용된 방식은 XML과 JSON
- XML(eXtensible Markup Language)
  - HTML은 브라우저가 해석하지만 xMl은 개발자나 프레임워크가 해석
  - XML은 구조적
  - JSON보다 인간이 읽기가 쉽지만 용량이 큼
  - 프레임워크의 설정 파일에 많이 이용되어 있는데 클라우드 환경에서는 이 방식보다 YAML을 선호
- JSON(Javascript Object Notation)
  - 자바스크립트의 객체 표현 방식을 이용
  - XML보다 경량이지만 인간이 읽기가 어려움
  - 인간이 읽기가 어렵기 때문에 설정 파일에 사용하기는 어렵고 데이터 전송에 많이 사용함
  - 스마트폰 운영체제의 데이터 전송 방식은 전부 JSON

### REST(REpresentational State Transfer)
- 분산 하이퍼미디어 시스템을 위한 소프트웨어 아키텍처의 형식
- 자원을 정의하고 자원에 대한 주소를 지정하는 방법 전반을 일컫는 말로 웹 상의 자료를 HTTP 위에서 SOAP(Simple Object Access Protocol)이나 쿠키를 통한 세션 트래킹같은 별도의 전송 계층없이 전송하기 위한 아주 간단한 인터페이스
- REST원리를 따르는 시스템을 RESTful 하다라고 함
- 6가지 제약조건
  - Client - Server 구조
  - Stateless(무상태): 클라이언트가 서버에 요청을 보낼 때 이전 요청의 영향을 받지 않아야 함
  - Cacheable Data: 서버에서 리소스를 리턴할 때 캐시가 가능한지 아닌지를 명시해야 하는 것인데 HTTP에서 cache-control 이라는 헤더에 리소스의 캐시 여부를 명시할 수 있음
  - Layered System: 여러 개의 레이어로 된 서버를 사용할 수 있음, 클라이언트는 이 사실을 알 필요가 없음. 하나의 시스템을 여러 개의 애플리케이션으로 분리해서 구현하기도 하고 인증 서버, 캐싱 서버, 로드 밸런서를 거쳐서 응답을 하기도 함
  - A Uniform Interface: 일관성있는 인터페이스를 가져야 함, HTML과 JSON두가지 형태의 데이터를 사용하는 것은 안됨, 동일한 컨텐츠를 사용하는 경우 동일한 URL을 사용하는 것을 권장
  - http://www.ex.com/todo: GET방식이면 가져오기, POST 방식이면 삽입 PUT이면 수정 DELETE이면 삭제 이렇게 HTTP 메서드로 작업을 구분
  - Code-On-Demand: 선택 사항으로 클라이언트는 서버에 코드를 요청할 수 있고 서버가 리턴한 코드를 실행할 수 있음

## Django REST Framework
- REST API를 만들 수 있는 프레임워크
- 설치 `pip install djangorestframework`

### 프로젝트 생성
- `django-admin startproject 프로젝트이름 경로`

### 애플리케이션 생성
- 프로젝트의 manage.py 파일이 있는 디렉터리에서 수행
- `python manage.py startapp 애플리케이션이름`

### settings.py 파일 수정
- INSTALLED_APPS 부분에 rest_framework와 자신의 애플리케이션 등록
- DATABASES 부분, TIME_ZONE 수정
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'rest',
        'USER': 'root',
        'PASSWORD': '0000',
        'HOST': '127.0.0.1',
        'PORT': ''
    }
}

TIME_ZONE = 'Asia/Seoul'
```
### urls.py 파일을 수정해서 example로 시작하는 url에 대한 처리는 apiapp의 urls.py에서 처리하도록 수정
- 프로젝트에 여러 개의 애플리케이션 존재하는 경우 프로젝트에서 모든 요청을 처리하도록 하면 프로젝트의 urls.py 가 너무 복잡해지므로 요청을 처리하는 로직이나 url 설정을 애플리케이션 단위로 분할하는 것이 좋음
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('example/',  include('apiapp.urls')),
]
```
### 요청을 만들고 JSON을 리턴하는 코드를 작성
- apiapp 디렉터리에 urls.py 파일을 추가하고 작성
```python
from django.urls import path
from .views import helloAPI

urlpatterns = [
    path("hello/", helloAPI),
]
```
- apiapp 디렉터리의 views.py 파일에 helloAPI 함수를 추가
```python
from django.shortcuts import render # 템플릿 엔진을 이용해서 HTML 출력에 사용
from rest_framework.decorators import api_view
from rest_framework.response import Response # json 데이터 생성에 사용

# GET 방식으로 온 요청만 처리
@api_view(['GET'])
def helloAPI(request):
    return Response("Hello REST API")
```
- 관리자용 테이블을 생성
```python
python manage.py makemigrations
python manage.py migrate
```
- 확인
  - 웹서버를 실행: `python manage.py runserver 127.0.0.1:80`
  - 브라우저에서 확인: http://127.0.0.1/example/hello/

### Response
- 응답 결과를 만들기 위한 클래스
- 인스턴스를 생성할 때 첫번째 매개변수가 클라이언트에게 전송될 데이터
- status는 상태 코드
- 주요 상태 코드
  - 200: OK
  - 201: created - 요청은 처리되어서 새로운 리소스를 생성
  - 202: Accepted - 요청은 접수되었지만 처리가 완료되지 않음
  - 3xx: 리다이렉션 중
  - 400: 잘못된 요청
  - 401: 권한이 없음
  - 403: 권한 처리 이외의 사유로 리소스에 대한 액세스가 금지
  - 404: 지정한 리소스를 찾을 수 없음, 서버에서 처리하는 로직을 찾을 수 없음
  - 500: 내부 서버 오류
- 응답 결과를 전송할 때 상태 코드를 같이 전송해서 정상 처리 여부를 알려주는 것이 좋음