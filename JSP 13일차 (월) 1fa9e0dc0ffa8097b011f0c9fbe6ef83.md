# JSP 13일차 (월)

날짜: 2025년 5월 26일

# `EX01`

```python
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<%
	if(session.getAttribute("USERID") == null){
%>
	<form action = "EX02.jsp" method = "post">
	아이디: <input type = "text" name = "userid">
	비밀번호: <input type = "password" name = "userpassword">
	<input type ='submit' value = "로그인">
	
	</form>
	<%
	}else{
	%>
		<%= session.getAttribute("USERNAME") %>
		<a href = "EX03.jsp"> [로그아웃] </a><br/>
		<a href = "EX04.jsp">  [회원수정]</a>
		<%
	}
		%>

</body>
</html>
```

# `EX02`

```python
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ page import = "common.MemberDTO" %>
<%@ page import = "common.MemberDAO" %>    
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>

<%
	String uid = request.getParameter("userid");

	String upass = request.getParameter("userpassword");

	MemberDAO dao = new MemberDAO();
	
	// MemberDTO getMemberDTO 메서드 호출
	MemberDTO dto = dao.getMemberDTO(uid, upass);
	
	dao.close();
	
	if(dto.getId()!=null){
		session.setAttribute("USERID", dto.getId());
		session.setAttribute("USERNAME", dto.getName());
		session.setAttribute("USERPW", dto.getPassword());
		
		response.sendRedirect("EX01.jsp");
	}

	
%>

</body>
</html>
```

# `EX03`

```python
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
	session.removeAttribute("USERID");
	session.removeAttribute("USERNAME");
	session.removeAttribute("USERPW");
	
	session.invalidate();
	
	response.sendRedirect("EX01.jsp");
	
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>

</body>
</html>
```

# `EX04`

```python
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ page import = "common.MemberDTO" %>
<%@ page import = "common.MemberDAO" %>    
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>

<%
	String uid = (String)session.getAttribute("USERID");

	MemberDAO dao = new MemberDAO();
	
	MemberDTO dto = dao.getMemberById(uid);
	
	String uid1 = dto.getId();
	
	String upw1 = dto.getPassword();
	
	String uname1 = dto.getName();
	
%>

	<form action = "EX05.jsp" method = "post">
	<input type = "hidden" name = "uid1" id = "id" value = "<%= uid1 %>">
	
	<label> 비밀번호 </label>
	<input type= "password" name = "upw1" id ="password" value = "<%= upw1 %>">
	
	<label> 이름 </label>
	<input type = "text" name = "uname1" id= "name" value = "<%= uname1 %>">
	
	<input type = 'submit' value = "수정"/>
	
	</form>
	
	<form action = "EX06.jsp" method = "post">
	<input type = "hidden" name = "uid1" id="id" value = "<%= uid1 %>">
	
	<input type= 'submit' value = "회원탈퇴"/>
	
	</form>

</body>
</html>
```

# `EX05`

```python
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ page import = "common.MemberDAO" %>    
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>

<%

	MemberDAO dao = new MemberDAO();

	String id = request.getParameter("uid1");
	
	String password = request.getParameter("upw1");
	
	String name = request.getParameter("uname1");

	int result = dao.updateMember(id, password, name);
	
	if(result >0){
		out.println("<p> 수정 완료 </p>");
	}
	else{
		out.println("<p> 수정 실패 </p>");
	}
%>

<a href = "EX03.jsp"> 로그인 화면 </a>

</body>
</html>
```

# `EX06`

```python
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ page import = "common.MemberDAO" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<%
	MemberDAO dao = new MemberDAO();

	String id = request.getParameter("uid1");
	
	int result = dao.deleteMember(id);
	
	if( result >0){
		out.println("<p> 탈퇴 성공 </p>");
	}
	else{
		out.println("<p> 탈퇴 실패 </p>");
	}
%>

</body>
</html>
```