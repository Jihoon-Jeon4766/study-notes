# JSP 4일차 (화)

날짜: 2025년 5월 13일

# `Quiz 2`

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ page import = "java.util.Random" %> 

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title> Quiz 2 </title>
</head>
<body>

<%
	Random rand = new Random();

	int randomNumber = rand.nextInt(100); 
	String result = (randomNumber % 2==0) ? "짝수" : "홀수";

%>

0부터 99 사이의 난수 : <%= randomNumber %> 
<p> 결과 : <%= result %>

</body>
</html>

```

# `Quiz 3`

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%!
public int factorial(int num){
    int fac = 1;
    for (int i =1; i<= num; i++){
        fac *= i;
    }
    return fac;
}
%>
    
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title> Quiz 3</title>
</head>
<body>

<%
int data = factorial(5);
%>

표현식 1 > 입력값 5! : <%= data %> <br>
표현식 2 > 입력값 7! : <%= factorial(7) %> 
</body> 
</html>
```

# `Quiz 4`

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>구구단 표 (2단부터 9단까지)</title>
</head>
<body>

	<h2>구구단 표 (2단부터 9단까지)</h2>

	<table border="1">
	
	<tr>
		<% for(int i = 2; i <= 9; i++) { %>

	</tr>
		
			  <tr>
				<% for(int j = 1; j <= 9; j++) { %>
				
					<td>
					
					//java 표현식
					<% out.println(i + "*" + j + "=" + i*j); %>
					
					//JSP 표현식
					<%= i %> X <%= j %> = <%= i*j %>
					
					</td>
			
				<% 
           }
	      }
         %>

		</tr>

	</table>

</body>
</html>
```

# `Quiz 5`

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title> 1부터 5까지의 숫자들에 대한 곱셉표를 출력 </title>
</head>
<body>
 
<h2> 곱셈표 (1부터 5까지) </h2>

<table border ="1">
	<tr>
		<th>*</th>
		<%
			for(int i=1; i<=5; i++){
		%>
			<th> <%= i %></th>
			
			<%
			}
			%>
	</tr>
			
			<%
			for(int i =1; i<=5; i++){
			%>
			<tr>
				<th><%= i %></th>
					<%
					for(int j=1; j<=5; j++){
					%>
					
						<td><%= i*j %></td>
					<%
					}
					%>
			</tr>
			<%
			}
			%>
	

</table>

</body>
</html>
```

# `내장 객체(Implicit Object)`

**JSP 페이지에서 별도의 선언 없이 기본으로 내장 되어 있어 바로 사용할 수 있는 객체**

| 내장 객체 | 설명 |
| --- | --- |
| request | 웹 브라우저의 요청 정보를 저장 |
| response | 웹 브라우저의 요청에 대한 응답 정보를 저장 |
| out | JSP 페이지의 출력할 내용을 가지고 잇는 출력 스트림 |
| session | 하나의 웹 브라우저 내에서 정보를 유지하기 위한 세션 정보를 저장 |
| application | 웹 애플리케이션 Context의 정보를 저장 |
| pageContext | JSP 페이지에 대한 정보를 저장 |
| page | JSP 페이지를 구현한 자바 클래스 |
| config | JSP 페이지에 대한 설정 정보 |
| exception | JSP 페이지에서 예외가 발생한 경우 사용 |

# `내장객체의 영역`

**JSP 페이지에서 다양한 범위에서 데이터를 저장하고 공유할 수 있는 영역을 의미**

**application** : 웹 애플리케이션 전체에서 공유되는 데이터 저장 영역

**session** : 특정 사용자와의 세션 동안 공유되는 데이터 저장 영역

**request** : 현재 HTML 요청에 대한 데이터 저장 영역

**page**: 현재 JSP 페이지의 스크립트와 서블릿에서 사용되는 데이터 저장 영역

# `Form 태그와 파라미터 처리`

**form 태그** : HTML 문서에서 사용자 입력을 수집하는데 사용

**Parameter** : 클라이언트가 서버로 전송한 데이터를 의미

```java
<form action="EX02.jsp" method="past">
	성함 : <input type = "text" name = "name"> <br>
	나이 : <input type = "text" name = "age"> <br>
	<intput type = "submit" value = "Submit">

</form>
```

**action** : form 데이터를 제출할 URL로 지정

**method** : 데이터를 서버로 제출하는 http를 전송

```java
<body>

<%
	String name = request.getParameter("name");
	String age = request.getParameter("age");
%>

<p> Name : <%= name %></p>
<p> age : <%= age %></p>	
</body>
```

**getParameter :** form에 저장된 데이터를 가져오기 위한 메서드