# JSP 1일차 (목)

날짜: 2025년 5월 8일

# `웹(Web)`

**웹은 World Wide or W3** 의 줄임말로서 인터넷 상에서 동작하는 하나의 서비스로

웹을 이해하기 위해서 반드시 알아야 하는 것이 바로 하이퍼텍스트 (HyperText)입니다.

# `하이퍼텍스트 (HyperText)`

**하이퍼텍스트(HyperText)**는 클릭하면 무언가로 연결되는 것이 바로 하이퍼텍스트의 역할로

웹은 이와 같은 하이퍼텍스트 구조를 활용해서 인터넷 상에 있는 수많은 정보들을 연결해주는 서비스를 말하는 것입니다.

# **`웹 프로그래밍`**

**http(Hyper Text Transfer Protocol)** 프로토콜 통신하는 클라이언트 프로그램 또는 서버 프로그램을 개발하는 것으로 일반적으로 사용자의 웹 브라우저를 통해 사용 할 수 있는 웹 프로그램을 개발하는 것을 의미한다.

웹 프로그래밍의 영역으로는 **Client Side (Front -End)** 영역과 **Server Side (Back- End)** 영역으로 구분된다.

**Front End** 영역에서는 웹 페이지를 사용하는 사용자의 User Interface 등을 구현한다.

**Back- End** 영역에서는 사용자 요청에 따른 데이터 처리 및 응답 데이터 생성 등의 작업을 수행한다.

# `Server, Client(*중요)`

**Client** : 데이터를 요청하는 컴퓨터           **Request** : 데이터를 요청하는 행위

**Server** : 데이터를 제공하는 컴퓨터          **Response** :  데이터를 제공하는 행위

**Client      → (Request)     Server**

**Client      ← (Response)  Server**

# `HTTP(Hyper Text Transfer Protocol)`

**//Protocol = 통신 규약**

**//TCP = (Transmission Control Protocol)  전송 제어 프로토콜**

**//IP = (Internet Protocol) 인터넷 프로토콜**

인터넷상에서 데이터를 송수신하기 위한 통신 약 ( Client & Server Model Protocol)

**HTTP는 TCP / IP** 기반의 통신을 진행하며, 기본 포트번호로 TCP / **80번을 사용**

**HTTP**는 어떠한 종류의 데이터든지 전송할 수 있도록 구현됨.

**WEB Client :** 웹 브라우저 ( 크롬, 엣지, 사파리, 웨일)

**WEB Server :** 웹 서버 서비스 ( Apache, Nginx, IIS)

# `HTTP (Requset & Response)`

**HTTP Requset** 

웹 클라이언트에서 웹 서버로 자원을 요청 (URL)

다양한 메서드 방식을 지원하며, 역할이 다르다.

| Method | 설명 | CRUD 역할   |
| --- | --- | --- |
| GET   | 정보요청  | READ |
| POST  | 데이터 전송 | Create |
| PUT | 데이터 변경 요청 | Update |
| DELETE  | 데이터 삭제 | Delete |
| OPITIONS | 지원하는 Method 정보 요청 |  |

**HTTP Response**

웹 클라이언트의 Requset에 대한 처리를 진행하고, 해당 결과를 응답

응답 코드에 따라 웹 클라이언트에서 요청에 대한 결과를 보여준다.

| CODE  | 의미 | 설명 |
| --- | --- | --- |
| 1xx |  Information | 임시응답, 지속적인 통신 진행 |
| 2xx | Success  | 클라이언트의 요청이 성공적으로 처리 되었음 (200 ok) |
| 3xx | Rediraction    | 요청을 처리 할 문서가 이동되었음을 알림 (301 Object Moved) |
| 4xx | Client Error | 클라이언트가 서버에 존재하지 않는 페이지를 요청 (404 Page Not Found |
| 5xx | Server Error | 서버에서 요청을 처리하는 중 오류가 발생( 500 Internal Server Error) |

# `WEB Server`

**Static Page (정적 페이지) - 저장**

클라이언트의 요청에 항상 동일한 응답을 하는 페이지 HTML, JavaScript, CSS, 이미지 등으로 이루어진 페이지 하이퍼링크를 통해 문서를 연결하고 보여주는 것이 목적 게시판이나 회원가입 기능 등이 없는 단순한 홈페이지 웹 사이트의 가장 기초적인 형태.

**WEB Server(웹 서버)**

웹 클라이언트의 요청을 받아 처리하는 서버

주로 HTML, JavaScript, CSS 이미지 등의 정적 페이지를 처리 ASP, JSP, PHP 등의 동적 페이지 처리는 WAS로 처리를 넘김 대표적인 WEB Server의 종류 : Apache, Nginx, IIS

# `WAS Server`

**Dynamic Page (동적 페이지) -전처리 처리**

클라이언트의 요청이 있을 때 마다 다른 응답을 주는 페이지(누가, 언제, 어떻게) 요청을 했는지에 따라 응답 결과가 달라진다. Client의 다양한 요청에 따라 상황에 맞는 적절한 처리가 가능하다. 회원가입, 로그인, 게시판 기능이 있는 홈페이지 서버측에서 데이터 처리를 담당하는 서버가 추가로 요구 된다.

**WAS Server ( 웹 어플리케이션 서버)**

동적 페이지처리 요청을 받아 처리하고 결과를 WEB으로 반환 Dynamic Page 구성 ( 특정 사용자의 데이터를 불러와 표시) DB와 연동하여 데이터 조회, 생성, 수정, 삭제 등의 기능을 수행대표적인 WAS Server의 종류 : Tomcat, JBoss, Jeus, Jetty

# **`서블릿(Servlet)`**

자바로 작성된 서버측 프로그램을, 클라이언트의 요청을 처리하고 응답을 생성하는 역할을 하여 웹 어플리케이션을 개발할 수 있도록 만드는 기술

# **`Jsp(Java Server Pages)`**

자바로 작성된 웹 페이지를 동적으로 생성하는 기술로, HTML과 자바 코드를 혼합하여 서버에서 실행되는 웹 어플리케이션을 개발

# `Apache Tomcat`

JSP와 서블릿등 동적 웹 개발에 필요한 기술을 지원하는 웹 어플리케이션 서버

**톰캣 연동 설정**

이클립스 뷰 아래 Server 클릭 → Servers 뷰에서 아래 링크 클릭해서 서버 생성 → 서버 생성창에서 [Apache] → [Tomcat v 10.1]선택후 Next 클릭 → Browse 버튼 클릭하여 톰캣이 설치된 폴더 선택 → Finish

Server가 켜져있으면 Request 를 요청해도 페이지가 없기에 404 오류가 나오게 되고,

Server가 꺼지면 사이트 연결할 수 없게 나오게 된다.

# `프로젝트 구조 확인`

**Web** - 프로젝트 폴더

**Java Resources** - 자바 소스 코드를 저장하는 곳

**webapp** - JSP 파일의 위치를 담는 곳

**lib** -외부 라이브러리를 담는 곳.

**web.xml** -서블릿 매핑을 위한 웹 어플리케이션의 배포 설정을 정의하는 곳

# `HTML(Hyper Text Markup Language)`

**HTML 은 Hyper Text Markup Language** 의 약어로 웹페이지를 만드는데 사용하는 기본적으로 사용되는 마크업 언어이다.

**HTML 기본 태그**

| 태그 | 기능 |
| --- | --- |
| <html> | html 문서의 시작을 알림 |
| <head> | html 문서의 필요한 사항( 웹 브라우저 제목 <title>, 한글 문자셋<meta>등..) |
| <meta> | html문서의 내용, 키워드,작성자,사용할 문자셋 등 문서의 포괄적인 내용을 기재 |
| <title> | 웹 브라우저의 상단 탭에 나타나는 문서의 제목 |
| <body> | 웹 브라우저 메인 화면에 들어갈 내용물들(text,image,video등) |

# `CSS( Cascading Style Sheets)`

**CSS**는 HTML 태그를 보조하여 웹 페이지를 꾸미는 역할로 폰트 글꼴, 폰트 색, 폰트 크기 등 을 지정하며, 웹 페이지의 배경 색상, 배경 이미지를 삽입하고 글자나 이미지 등의 요소를 배치하는 대도 사용됨.

# `단락 나누기 → 단락 태그 [p]`

# `글씨 두껍게 하기 → 글씨 두께 태그 [b]`

```
<h3>리그오브레전드</h3>
<h5>제작 라이엇 게임즈</h5>

<h2><b>리그 오브 레전드</b>는 세계 최고의 <b>MOBA(Multiplayer Online Battle Arena)</b>게임입니다. 끝없이 이어지는 실시간 전투와 협동을 통한 팀플레이
RTS와 RPG를 하나의 게임에서 동시에 즐길 수 있는 새로운 장르의 온라인 게임입니다. 두 팀은 각기 독특한 특성과 플레이스타일을 자랑하는 강력한
챔피언을 소환하여 다양한 모드의 전장에서 정면 대결을 펼칩니다. 신규 챔피언이 끊임없이 추가되며, 지속적인 업데이트가 이루어지고 흥미진진한
e 스포츠 대회의 중심이기도 한 <b>리그 오브 레전드에서 많은 동료 소환들과 함께 박진감 넘치는 전투를 즐겨보세요!</h2>

```

# `글 제목 만들기 => 제목 태그[h1 -> h6]`

```
<h1>글 제목1</h1>
<h2>글 제목1</h2>
<h3>글 제목1</h3>
<h4>글 제목1</h4>
<h5>글 제목1</h5>
<h6>글 제목1</h6>

```

# `줄 바꿈과 공백 삽입하기 -> 엔터(br)와 스페이스바(&nbsp;)<br>`

-br 태그는 줄 바꿈 처리 된다.<br>

```
<h3><b>리그오브레전드</b></h3>

<h5>제작 라이엇 게임즈</h5>
<h2><b>리그&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;오브레전드</b>는 세계 최고의 <b>MOBA(Multiplayer Online Battle Arena)</b>게임입니다.</h2>

```