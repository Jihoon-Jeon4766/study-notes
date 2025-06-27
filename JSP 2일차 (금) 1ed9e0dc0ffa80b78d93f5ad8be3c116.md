# JSP 2일차 (금)

날짜: 2025년 5월 9일

# `Table`

<table>

<tr> (행)

<th> (열 제목)

<td> (열)

# `테이블의 행과 열 합치기`

th 태그 

<rowspan = “행너비”>

<colspan = “열너비”>

**<from>**

**intput** 

**</from>**

# `라디오버튼과 체크박스` Ex18.html

<input type = “radio”>

<input type = “checkbox”>

<body>

내국인 :<input type =*"radio"* name =*"test1"*> 예

      <input type =*"radio"* name =*"test1"*> 아니오<br>

취&nbsp;&nbsp;&nbsp;미 :

<input type = *"checkbox"*>멍때리기

<input type = *"checkbox"*>음악감상

<input type = *"checkbox"*>프로그래밍

<input type = *"checkbox"*>영화보기

<input type = *"checkbox"*>산책 및 하이킹

</body>

# `선택박스만들기`

-선택 박스 태그 <select>

-선택 항목명 태그 <option>

```java
<body>
<form>
<select>

<option>1</option>
<option>2</option>
<option>3</option>
<option>4</option>
<option>5</option>

</select>
</form>
</body>
```

# `다중 입력 창 만들기-입력 창 태그` Ex20.html

<textarea rows =”행” cols=”열”>

```java
<body>

코드입력:<br>

<textarea rows=*"5"* cols=*"70"*></textarea>

</body>
```

# `버튼 만들기`

```java
<form>

<button type=*"button"*>확인</button>

<button type=*"button"* onclick="location.href='https://www.naver.com'">확인1</button>

</form>
```

# `스크립트 요소`

```java
<%!
String str1 ="Hello";
String str2= "World";
%>
```

# `지시어(Directive)`

JSP 페이지를 자바(서블릿)코드로 변환하는데 필요한 정보를 JSP엔진에 제공

```java
<%@ page language=*"java"* contentType=*"text/html; charset=UTF-8"*

pageEncoding=*"UTF-8"*%>
```

<%@ 지시어 종류 속성1 = “값1” 속성2=”값2”,…. %>

## **page 지시어**

JSP페이지에 대한 정보를 설정

| 속성 | 내용 |
| --- | --- |
| info | 페이지에 대한 설명을 입력 |
| language | 페이지에서 사용할 스크립팅 언어를 지정 |
| content Type | 페이지에서 생성할 MME 타입을 지정 |
| pageEncoding | charset과 같이 인코딩을 지정 |
| import | 페이지에서 사용할 자바 패키지와 클래스를 지정 |
| session | 세선 사용 여부를 지정 |
| buffer | 출력 버퍼의 크기를 지정 |
| autoFlush | 출력 버퍼가 모두 채워졌을 때 자동으로 비울 지를 결정 |
| timeDirectiveWhitespaces | 지시어 선언으로 인한 공백을 제거할지 여부를 지정 |

# `page 지시어`

**import**

```java
<%@ page import = *"java.util.Scanner"* %>  

<%@page import = “클래스명”%>
```