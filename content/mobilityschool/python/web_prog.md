---
title: Web Programming
weight: 11
---
- 웹 애플리케이션은 수행되는 위치에 따라 Front End(Client)와 Back End(Server)로 분류
- Front End
  - Back End와 사용자 사이에서 보여지는 부분
  - Web에서는 HTML, CSS, JavaScript 언어를 이용해서 구현을 하는데 최근에는 프레임워크 형태로 제공되는 jQuery(사용을 금기시), Angular(업데이트 더 이상 진행되지 않음), react, vue, bootstrap(react나 vue안에서 사용되는 경우가 많음) 등을 많이 이용
  - Java, Kotlin, Objective-C, Swift, JavaScript, Python 등도 Front End 프로그래밍이 가능한 언어
- Back End
  - 애플리케이션을 동적이고 대화형으로 만들기 위한 숨은 부분
  - 클라이언트의 요청을 받아서 처리하기 위한 부분
  - 서버를 제작하기 위한 프로그래밍 언어(Java, Python, PHP, C#, JavaScript, Go 등) 과 데이터 저장 기술(RDBMS, NoSQL, File 등)과 SW공학 등의 기술을 가지고 제작
  - 최근에는 프레임워크를 사용하는 경우가 많음: Spring, Django, Express.js, FastAPI 등
- 일반적인 Web Application의 동작
  - 클라이언트에서 최초 요청(request)을 서버에 전달하고 서버는 요청을 받아서 처리한 후 그 응답(response)을 HTML 형태로 클라이언트에게 전송하고 이후 추가적인 자원이 필요하면 다시 요청을 한 후 서버가 응답을 하는 구조
  - 최근에는 서버가 클라이언트에게 HTML을 전송하지 않고 문자열 형식으로 만들어진 데이터를 전달하고 클라이언트에서 해석을 해서 출력하는 방식을 많이 사용
  - 서버가 HTML을 전송하게 되면 클라이언트가 다양한 형태로 존재하는 경우 서버를 여러 개 준비를 해야 할 가능성이 생김
- web 3.0
  - 시맨틱 웹의 개념: 컴퓨터가 정보 자원의 뜻을 이해하고 논리적 추론까지 가능한 것
  - 속도와 플랫폼 변화
  - 인공지능
  - 애플리케이션의 진화: open API, SOA(Service Oriented Architecture) 등의 새로운 플랫폼 등장과 Mesh Up
- WOA(Web Oriented Architecture)
  - 웹 기반 서비스 구조
  - Restful: 동일한 요청에 대해서 동일한 URL을 사용할 수 있도록 하는 것
- 프레임워크를 이용한 개발을 권장
  - 지금의 프로그램은 너무 복잡
  - 복잡한 프로그램을 만들기 위해서 알아야 할 기술이 너무 많음

### URL(Uniform Resource Locator)
- 클라이언트가 서버에 존재하는 자원을 요청하는데 필요한 네트워크 서비스의 표현
- 기본 형식 `[프로토콜]://[호스트][:포트]/[경로]/[QueryString - Parameter]#Fragment`
- 프로토콜: 이 부분이 생략되고 //로 시작하면 상황에 따라 http나 https로 프로토콜을 추가
- 호스트: 컴퓨터를 구분하기 위한 이름으로 IP나 도메인
- 포트: 컴퓨터 내에서 애플리케이션을 구분하기 위한 번호인데 프로토콜의 기본 포트인 경우는 생략이 가능
- 경로: 서버에게 요청을 하는 구분하기 위한 문자열로 설정에 따라 생략이 가능
- Query String: 클라이언트가 서버에게 전송하는 데이터
- Fragment: 문서 내에서 이동할 이름

### URL을 바라모는 측면
- 웹 클라이언트에서 웹 서버에 존재하는 Application에 대한 API(Application Programming Interface)
- URL을 RPC(Remote Procedure Call)로 바라보는 시각이 있고 다른 하나는 REST(Representational State Transfer)로 바라보는 시각
- RPC - 원격 프로시져 호출
  - 클라이언트가 네트워크 상에 있는 서버가 제공하는 API 함수를 호출하는 것
  - URL의 경로를 API함수 이름으로 하고 쿼리 스트링을 함수의 매개변수로 간주해서 웹 클라이언트에서 URL 전송하는 것은 웹 서버의 API함수를 호출하는 것으로 인식하는 것
  - 이 경우는 함수의 이름이 대부분 동사
  - search라는 API함수에 test라는 데이터를 전송: `http://blog.ex.com/search?q=test&debug=true`
- REST
  - 웹 서버에 존재하는 요소들을 모두 리소스로 정의하고 URL을 통해 웹 서버의 특정 리소스를 표현한다고 하는 개념
  - 리소스는 시간이 지남에 따라 상태가 변할 수 있기 때문에 클라이언트와 서버 간의 데이터 교환을 리소스 상태의 교환으로 간주
  - 리소스에 대한 조작을 HTTP메서드로 구분: GET, POST, DELETE, PATCH
  - 웹 클라이언트에서 URL을 전송하는 것이 웹 서버에 있는 리소스 상태에 대한 데이터를 주고 받는 것으로 간주
  - `http://blog.ex.com/search/test`
- 단축 URL
  - URL을 간단하게 줄여서 사용하는 방식
  - `http://ex.com/index.php?page=foo -> http://ex.com/foo`
  - `http://ex.com/products?category=2&pid=25 -> http://ex.com/products/2/25`

### HTTP 메서드
- get
  - 데이터를 요청할 때 사용하는 것으로 default
  - 클라이언트에서 서버에게 데이터를 전달할 때 URL 뒤에 데이터를 같이 전송
- 단점: 보안이 취약, 데이터 길이에 제한
- 장점: 자동 재전송
- 폼이 있다면 폼에 file, textarea, password가 있는 경우 get 방식으로 전송하면 안됨
- post
  - 데이터를 삽입할 때 사용하는 것으로 클라이언트에서 서버에게 데이터를 전송할 때 요청의 body에 숨겨서 전송하는 방식
  - 장점: 보안이 우수, 데이터 길이에 제한이 없음
  - 단점: 자동 재전송 기능이 없음
- head: 리소스 헤더 취득
- options: 리소스가 지원하는 메서드 취득
- trace: loopback 시험에 이용
- connect: 프록시 동작의 터널 접속으로 변경
- 예전에는 get과 post만 사용했는데 최근에는 put과 delete를 같이 사용

### 상태 코드
- 웹 서버와 통신에서는 클라이언트에게 상태 코드를 전송함
- 1xx: 정보 제공중
- 2xx: 정상 응답
- 3xx: 리다이렉션 중 - 완전한 동작을 위해서 추가적인 동작을 수행
- 4xx: 클라이언트 오류
- 5xx: 서버 오류