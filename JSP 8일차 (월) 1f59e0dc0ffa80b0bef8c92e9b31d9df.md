# JSP 8일차 (월)

날짜: 2025년 5월 19일

# `JDBC(Java DataBase Connectivity)`

**데이터베이스에 연결 및 작업을 하기 위한 자바 표준 인터페이스**

![image.png](JSP%208%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%8B%E1%85%AF%E1%86%AF)%201f59e0dc0ffa80b0bef8c92e9b31d9df/image.png)

## **라이브러리 추가 방법**

프로젝트에서 우측버튼 → properties → java build path → Library → ModulePath → Add External JARs… → ojdbc11

```java
package common;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.Statement;

public class JDBConnect {
    public Connection con; //데이터베이스와 연결 객체
    public Statement stmt; // 정적, 동적, Query를 실행하는 객체
    public PreparedStatement psmt; //정적, 동적, Query를 실행하는 객체
    public ResultSet rs; //Query문에 결과를 저장하는 객체

    // 생성자
    public JDBConnect() {
        try {
		        //forName으로 OracleDriver 로드하기(호출)하기..
            Class.forName("oracle.jdbc.OracleDriver"); 
			
            String url = "jdbc:oracle:thin:@localhost:1521:xe";
            String id = "jun";
            String password = "jsp2025";
            con = DriverManager.getConnection(url, id, password);

            System.out.println("DB 연결 성공 (생성자)");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // 자원 해체 메서드 
    public void close() {
        try {
            if (rs != null) rs.close();
            if (stmt != null) stmt.close();
            if (psmt != null) psmt.close();
            if (con != null) con.close();
            
            System.out.println("JDBC 자원 해체");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

## OracleDriver 로드 실패 경우..

![스크린샷 2025-05-19 오후 6.03.55.png](JSP%208%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%8B%E1%85%AF%E1%86%AF)%201f59e0dc0ffa80b0bef8c92e9b31d9df/f422b205-ad01-4160-b29f-9d656cd0eeed.png)

web →apache-tomcat →conf → server.xml / context.xml

커넥션 풀(Connection Pool)

DB와 미리 connection을 해놓은 객체들을 pool에 저장해 두었다가 클라이언트의 요청이 오면 connection을 빌려주고 처리가 끝나면 다시 connection을 반납 받아 pool에 저장하는 방식..

```java
package common;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.Statement;

import javax.naming.Context;
import javax.naming.InitialContext;
import javax.sql.DataSource;

public class DBConnPool {
	public Connection con;
	public Statement stmt;
	public PreparedStatement psmt;
	public ResultSet rs;
	
	public DBConnPool() {
		try {
			Context initCtx = new InitialContext();
			Context ctx = (Context)initCtx.lookup("java:comp/env"); 
			DataSource source = (DataSource)ctx.lookup("dbcp_myoracle");
			
			con = source.getConnection();
			
			System.out.println("DB 커넥션 풀 연결 성공");
		}catch (Exception e) {
			// TODO: handle exception
			System.out.println("DB 커넥션 풀 연결 실패");
			e.printStackTrace();
		}
	}
	public void close() {
        try {
            if (rs != null) rs.close();
            if (stmt != null) stmt.close();
            if (psmt != null) psmt.close();
            if (con != null) con.close();
            System.out.println("JDBC 자원 해체");
        } catch (Exception e) {
            e.printStackTrace();
        }
       
	}

}

```

# `EX02` `Query문을 삽입해서 회원가입`

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>회원 가입</title>
</head>
<body>

<form action="EX03.jsp" method="post">
    <label for="id">아이디 :</label>
    <input type="text" name="id" id= "id" required><br><br>

    <label for="password">비밀번호 :</label>
    <input type="text" name="password" id= "password" required><br><br>

    <label for="name">이름 :</label>
    <input type="text" name="name" id="name" required><br><br>

    <input type="submit" value="회원가입">
</form>

</body>
</html>

```

# `EX03` `Query문을 삽입해서 회원가입`

```java

<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
<%@ page import = "java.sql.PreparedStatement" %>  
<%@ page import = "java.sql.Connection" %> 
<%@ page import="common.DBConnPool" %> 

  
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>

	<h2> 회원가입 테스트(executeUdate)사용)</h2>
	
	<%//form 데이터 받아오기
		String id = request.getParameter("id");
		String pass = request.getParameter("password");
		String name = request.getParameter("name");
		
		//DB에 연결해서 호출!
		DBConnPool pool = new DBConnPool(); //중요!!!!!!!!!!!
		
		String sql = "INSERT INTO member VALUES (?,?,?,sysdate)";
		
		//PreparedStatement() ->Query문 실행을 준비
		PreparedStatement psmt = pool.con.prepareStatement(sql);

		psmt.setString(1, id);
		psmt.setString(2, pass);
		psmt.setString(3, name);
		
		//executeUpdate() -> Query문 실행	
		//성공되면 1이 실패되면 0이 반환..	
		int inResult = psmt.executeUpdate();

		
		pool.close();
		
		if(inResult > 0){
			out.println("<p> 회원가입이 성공적으로 완료 </p>");
		}
		else{
			out.println("<p> 회원가입 실패! 다시 시도하세요 </p>");
		}
		
	%>

</body>
</html>
```