# JSP 6일차 (목)

날짜: 2025년 5월 15일

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>

<%@ page import = "java.util.Random" %> 

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title> 운세 결과 </title>
</head>
<body>

<h1> 오늘의 운세 결과 </h1>
<%
String userName = request.getParameter("name");

if (name != null && name.isEmpty(){
			session.setAttribute("userName",name);
}

String userName = (String) session.getAttribute("userName");

String fortunesMsg = getServletConfig().getInitParameter("fortunes");

Random rand = new Random();

int randomNumber = random.nextInt(5);

String result, colors;

if(randomNumber ==1){
	result= "매우 좋음";
	colors = "하늘색";
}else if(randomNumber ==2) {
	result =  "좋음";
	colors = "핑크색";
}else if(randomNumber ==3){
	result = "보통";
	colors ="노랑색";
}else if(randomNumber ==4){
	result = "한번 더!"
	colors = "초록색";
}else{
	result = "꽝";
	colors = "흰색";
}

	
%>

<p><%= fortunesMsg %></p>

<p><%= userName %>님! 환영합니다.</p>

<p>오늘의 운세 결과는 <%= result %>입니다.</p>

<p>오늘의 행운 컬러는 <%= colors %>입니다.</p>

<p>오늘도 화이팅!</p>

</body>
</html>
```

# `액션 태그 (Action Tag)`

**JSP에서 사용되는 특별한 태그**

```java
<jsp: Tag name>
```

# `include`

다른 JSP 페이지를 현재 페이지에 포함

```java
<jsp: include>
```

<%@ include file =”경로”> vs <jsp:include> 차이점 <표>

|  | include 지시어 | <jsp:include> 액션 태그 |
| --- | --- | --- |
| 형식 | <%@ include file =”경로”> | <jsp:include page = “”/> |
| 처리 시점 | 자바 소스로 변환 시 | 실행 시 |
| 기능 | 현재 파일에 삽입하여 하나의 파일로 생성 | 별도의 파일로 처리 |
| 데이터 구성 | 정적 데이터 구성 | 동적 데이터 구성 |
| 용도 | 여러 페이지에서 사용하는 변수를 지정하고 include 시킴 | 화면 레이아웃 모듈화시(top페이지 bottom 페이지를 include시킴) |

# `forward`

**현재 요청을 다른 페이지로 전달**

```java
<jsp: forward>
```

request 영역의 데이터를 공유하고 URL이 변경되지 않는다.

# `useBean, setProperty, getProperty`

**JavaBean 을 생성하거나 사용하며, 속성을 설정 및 값을 가져옴**

```java
<jsp:useBean id ="자바빈즈 이름" class = "클래스 명" scope= "저장될 영역">

<jsp:setProperty name = "자바빈즈 이름" property = "속성명(멤버 변수)">

<jsp:getProperty name = "자바빈즈 이름" property = "속성명(멤버 변수)">
```

# `param`

**forward 및 include 할 때 매개변수를 전달**

```java
<jsp: param>
```

String 만 전달 가능..