# Spring Boot 5일차 (화)

날짜: 2025년 6월 17일

# `MVC 패턴`

# **MVC Model 패턴 ★★★**

**모델(model), 뷰(view), 컨트롤러(controller)의 약자로 소프트웨어를 개발하는 방법론**

### **-모델(Model) (Entity / DTO/ Service.java)**

애플리케이션의 데이터와 비즈니스 로직을 담당

Spring Boot에서 모델은 데이터베이스와의 상호작용, 데이터 처리 등을 담당

주로 JPA를 이요해 Entity, DTO, Service  클래스를 구성

### **-뷰(View) (file.mustache)**

사용자에게 데이터를 시각적으로 표현하는 역할로 사용자 인터페이스(UI)를 구성하며, 모델의 데이터를 화면에 표시.

뷰는 사용자에게 정보를 시작적으로 표시하는 템플릿 파일로, 이는 HTML코드와 Mustache를 포함.

### **-컨트롤러(Controller) (Controller. java)**

사용자의 입력을 처리하고, 모델과 뷰 간의 상호작용을 조정.

사용자의 요청을 받아 적절한 모델을 업데이트하거나 뷰를 선택하는 웹 애플리케이션의 기능이 실질적으로 정의됨

Spring Boot에서는 @Controller 또는 @RestController로 구현되며, 사용자의 요청을 처리하고 모델 데이터를 가져와 템플릿 뷰로 전달하거나, JSON 응답을 반환한다.

JSON = JavaScript Object Notation -텍스트 기반의 데이터 형식..

**MVC Model 동작 순서**

1. 사용자 요청 → 2. 요청분석(Controller) → 3. 모델 호출 → 4. 데이터반환
→ 5. 데이터 처리 및 뷰 호출 → 6. 웹 브라우저 응답 → 7. 페이지확인

![image.png](JSP%2016%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%202009e0dc0ffa8092aa55dfc54827f617/image%201.png)

# `뷰 템플릿 (Mustache)`

**웹 페이지를 하나의 툴로 만들고 여기에 변수를 삽입해 서로 다른 페이지로 보여 주는 기술.**

**동적인 데이터를 HTML에 삽입해 사용자에게 보여주는 역할**

**프레젠테이션 로직을 담당 (ex. `if`, `for` 등을 통해 데이터 반복/조건 처리)**

### resources → templates → new → file

![스크린샷 2025-06-17 20.45.47.png](Spring%20Boot%205%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%202159e0dc0ffa80a09bdfd146978fc569/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-17_20.45.47.png)

### Install 클릭

![스크린샷 2025-06-17 20.48.51.png](Spring%20Boot%205%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%202159e0dc0ffa80a09bdfd146978fc569/6030aecc-419d-416d-86d5-9c308167ae1f.png)

![스크린샷 2025-06-17 20.50.01.png](Spring%20Boot%205%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%202159e0dc0ffa80a09bdfd146978fc569/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-17_20.50.01.png)

### **없다면 → 이거 설치**

![스크린샷 2025-06-17 20.51.16.png](Spring%20Boot%205%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%202159e0dc0ffa80a09bdfd146978fc569/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-17_20.51.16.png)

# `hi.mustache 만들기`

```java
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Document</title>
</head>
<body>
    <h1> Jun님, 반갑습니다. </h1>
</body>
</html>
```

# `controller 만들기`

![스크린샷 2025-06-17 21.01.08.png](Spring%20Boot%205%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%202159e0dc0ffa80a09bdfd146978fc569/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-17_21.01.08.png)

# `MvcController`

```java
package com.example.project.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class MvcController {

    @GetMapping("/hello")
    public String helloWorld(){
        return "hi";
    }
}

@GetMapping("/bye")
    public String byeWorld(Model model) {
        // 모델을 사용하기 위한 모델 추가
        model.addAttribute("username1", "Micheal");
        return "bye";
    }
}
```

 **`@Controller` 이 클래스가 controller 임을 선언하는 어노테이션이다.**

**`@GetMapping("/hello")`: 클라이언트가 `/hello` URL로 GET 요청을 보내면 아래의 `helloWorld()` 메서드가 실행됨**

**hi.mustache → return “hi”** 

[**application.properties](http://application.properties)** →  **.. 추가 ( 안 깨짐)**

```java
server.servlet.encoding.force=true
```

![스크린샷 2025-06-17 21.20.59.png](Spring%20Boot%205%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%202159e0dc0ffa80a09bdfd146978fc569/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-17_21.20.59.png)

# `결과화면 → [localhost8080/hello](http://localhost:8080/hello)`

![스크린샷 2025-06-17 21.26.27.png](Spring%20Boot%205%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%202159e0dc0ffa80a09bdfd146978fc569/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-17_21.26.27.png)

# **`클래스 자동 import 되게 하기`**

![스크린샷 2025-06-17 21.29.22.png](Spring%20Boot%205%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%202159e0dc0ffa80a09bdfd146978fc569/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-17_21.29.22.png)

![스크린샷 2025-06-17 21.30.21.png](Spring%20Boot%205%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%202159e0dc0ffa80a09bdfd146978fc569/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-17_21.30.21.png)

**MVC Model 동작 순서**

1. 사용자 요청 → 2. 요청분석(Controller) → 3. 모델 호출 → 4. 데이터반환
→ 5. 데이터 처리 및 뷰 호출 → 6. 웹 브라우저 응답 → 7. 페이지확인
- **사용자 요청**
    - 사용자가 웹 브라우저에서 `http://localhost:8080/hello` 주소로 접속하거나 요청을 보냄.
- **요청 분석 (Controller)**
    - Spring의 DispatcherServlet이 요청을 가로채고
    - `@GetMapping("/hello")`이 달린 `MvcController.helloWorld()` 메서드를 찾아 호출함.
- **모델 호출 ()**
- **데이터 반환 ()**
    - 단순히 `"hi"`라는 문자열(뷰 이름)만 반환함.
- **뷰 처리 및 뷰 호출**
    - 반환된 `"hi"`는 뷰 이름으로 인식됨.
    - Spring은 `src/main/resources/templates/hi.mustache` 파일을 찾아 HTML로 렌더링함.
- **웹 브라우저 응답**
    - 렌더링된 HTML이 HTTP 응답으로 사용자 브라우저에 전송됨.
- **페이지 확인**
    - 사용자 브라우저에 `hi.mustache` 내용이 표시됨. 예:
    - `<h1> 지훈님, 반갑습니다. </h1>` 같은 화면.