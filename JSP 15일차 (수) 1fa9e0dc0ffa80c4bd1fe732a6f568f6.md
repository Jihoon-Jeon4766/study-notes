# JSP 15일차 (수)

날짜: 2025년 5월 28일

# `JSP 표준 태그 라이브러리(JSTL)`

JSP에서 사용되는 조건문, 반복문 등을 처리해주는 태그를 모아 놓은 라이브러리

```java
<prefix: Tag name>
```

# `JSTL 태그 종류`

| 종류 | 기능 | 접두어 | URI |
| --- | --- | --- | --- |
| Core 태그 | 변수 선언, 조건문, 반복문, URL 처리 | C | jakarta.tags.core |
| Formatting 태그 | 숫자, 날짜, 시간 포맷 지정 | fmt | jakarta.tags.fmt |
| XML 태그 | XML 파싱 | x | jakarta.tags.xml |
| Function 태그 | 컬렉션, 문자열 처리 | fn | jakarta.tags.function |
| SQL 태그 | 데이터 베이스 연결 및 쿼리 실행 | sql | jakarta.tags.sql |

# `JSP 표준 태그 라이브러리(JSTL)`

**지시어**

```java
<%@ taglib prefix = "c" uri ="jakarta.tags.core" %>
```

https://mvnrepository.com/

jakarta.servlet.jsp.jstl

![스크린샷 2025-05-28 17.28.24.png](JSP%2015%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%201fa9e0dc0ffa80c4bd1fe732a6f568f6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-05-28_17.28.24.png)

>3.0.2 클릭

>jar (45 KB) 클릭

![스크린샷 2025-05-28 17.31.52.png](JSP%2015%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%201fa9e0dc0ffa80c4bd1fe732a6f568f6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-05-28_17.31.52.png)

>3.0.1 클릭

>jar (3.5 MB) 클릭

WEB-INF → lib → 붙여넣기

# `Core 태그`

**Core 태그는 변수 선언, 조건문, 반복문 등을 대처하는 태그를 제공함**

| 태그명 | 기능 |
| --- | --- |
| set | EL에서 사용할 변수를 설정 (=setAttribute()) |
| remove | 설정한 변수를 제거 (=removeAttribute()) |
| if | 조건문 사용 (else 사용X) |
| choose | 다중 조건문 사용 |
| forEach | 반복문 사용 |
| forTokens | 구분자로 분리된 토큰 처리할 때 사용 |
| import | 외부 페이지 삽입 |
| redirect | 지정한 경로로 이동(sendRedirect()) |
| url | 경로 설정 시 사용 |
| out | 내용을 출력 시 사용 |
| catch | 예외 처리 시 사용 |