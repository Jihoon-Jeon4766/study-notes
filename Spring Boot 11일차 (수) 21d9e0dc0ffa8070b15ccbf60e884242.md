# Spring Boot 11일차 (수)

날짜: 2025년 6월 25일

# `Mustache 문법`

**변수**

```java
{{변수명}}
```

조건문

```java
{{#변수}}...{{/변수}}
{{^변수}}...{{/변수}}
```

```java
@GetMapping("/example2")
    public String example2(Model model){
        model.addAttribute("isLogin",true);
        return "examples/example2";
    }
```

```java
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">

    <title>bye, world!</title>
</head>

<body>
{{>layout/header}}

<!--content-->
<div class="bg-dark text-white p-5">
 {{#isLogin}}
     <p> 로그인 상태</p>
 {{/isLogin}}
{{^isLogin}}
    <p> 로그인 해주세요~ </p>
{{/isLogin}}
</div>

{{>layout/footer}}

</body>
</html>
```

![스크린샷 2025-06-25 11.46.14.png](Spring%20Boot%2011%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%2021d9e0dc0ffa8070b15ccbf60e884242/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-25_11.46.14.png)

```java
@GetMapping("/example2")
    public String example2(Model model){
        model.addAttribute("isLogin",false);
        return "examples/example2";
    }
```

![스크린샷 2025-06-25 11.47.44.png](Spring%20Boot%2011%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%2021d9e0dc0ffa8070b15ccbf60e884242/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-25_11.47.44.png)

리스트

```java
{{#list}}...{/list}
```

```java
@GetMapping("/example3")
    public String example3(Model model) {

//        List<Map<String,String>> foods = new ArrayList<>();

//        Map<String,String> food1 = new HashMap<>();
//        food1.put("foodname","햄버거");
//
//        Map<String,String> food2 = new HashMap<>();
//        food2.put("foodname","피자");
//
//        Map<String,String> food3 = new HashMap<>();
//        food3.put("foodname","치킨");

//        foods.add(food1);
//        foods.add(food2);
//        foods.add(food3);

        List<Map<String, String>> foods = List.of(
                Map.of("foodname", "햄버거"),
                Map.of("foodname", "피자"),
                Map.of("foodname", "치킨")
        );

        for (Map<String, String> food : foods) {
            System.out.println(food);
        }

        model.addAttribute("foods", foods);

        return "examples/example3";
    }
```

# `→결과물`

![스크린샷 2025-06-25 18.26.37.png](Spring%20Boot%2011%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%2021d9e0dc0ffa8070b15ccbf60e884242/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-25_18.26.37.png)

중첩 객체 접근

```java
{{객체명.속성}}
```

```java
 @GetMapping("/example4")
    public String example4(Model model) {

        Map<String, String> user = Map.of("name", "전지훈", "email", "ejjdj8eewj@gamil.com");

        model.addAttribute("user", user);

        return "examples/example4";
    }
```

# `→ 결과물`

![스크린샷 2025-06-25 18.27.14.png](Spring%20Boot%2011%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%2021d9e0dc0ffa8070b15ccbf60e884242/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-25_18.27.14.png)

다른 템플릿 포함

```java
{{>layouts/header}}
{{>partials/footer}}
```

```java
@GetMapping("/example5")
    public String example5(Model model) {

        model.addAttribute("content", "이곳은 본문 입니다.");

        return "examples/example5";
    }
```

# `→ 결과물`

![스크린샷 2025-06-25 18.27.47.png](Spring%20Boot%2011%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%2021d9e0dc0ffa8070b15ccbf60e884242/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-25_18.27.47.png)

주석

```java
{{!주석}}
```

```java
//이건 보임
    //이건 안 보임
    @GetMapping("/example6")
    public String example6(Model model) {
        return "/examples/example6";
    }
```

# `→결과물`

![스크린샷 2025-06-25 18.28.10.png](Spring%20Boot%2011%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%2021d9e0dc0ffa8070b15ccbf60e884242/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-25_18.28.10.png)

HTML

{{{ → 3개 

```java
{{{content}}}
```

```java
//htmlContent 변수 선언 및 <strong> 지훈님! 환영합니다. </strong>
    @GetMapping("/example7")
    public String example7(Model model) {
        model.addAttribute("htmlContent", "<strong> 환영합니다. </strong>");

        return "/examples/example7";
    }
```

→결과물

![스크린샷 2025-06-25 18.29.25.png](Spring%20Boot%2011%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%2021d9e0dc0ffa8070b15ccbf60e884242/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-25_18.29.25.png)

# `롬복(Lombok)`

**코드를 간소화 하는 라이브러리로 코드 리팩터링 및 로깅 기능으로 대체 가능**

![스크린샷 2025-06-25 16.44.09.png](Spring%20Boot%2011%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%2021d9e0dc0ffa8070b15ccbf60e884242/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-25_16.44.09.png)

1. build.gradle → 라이브러리 다운

```java

```

1. dto → BoardForm

```java
package com.example.project.dto;

import com.example.project.entity.Board;
import lombok.AllArgsConstructor;
import lombok.ToString;

@ToString
@AllArgsConstructor
public class BoardForm {
    private String title;
    private String content;

    public Board toEntity() {
        return new Board(null, title, content);
    }
}
```

1. Entity → Board

```java
package com.example.project.entity;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.Id;
import lombok.AllArgsConstructor;
import lombok.ToString;

@ToString
@AllArgsConstructor
@Entity
public class Board {

    @Id
    @GeneratedValue
    private Long id;

    @Column
    private String title;

    @Column
    private String content;

}
```

롬복(Lombok)

정리

```java
@AllArgsConstructor : 클래스 내의 모든 필드를 매개변수로 
하는 생성자를 만드는 어노테이션

@ToString : toString()을 사용한 것과 동일한 어노테이션

@Sl4j : 로깅 기능을 사용하기 위한 어노테이션 "log,info()"

```