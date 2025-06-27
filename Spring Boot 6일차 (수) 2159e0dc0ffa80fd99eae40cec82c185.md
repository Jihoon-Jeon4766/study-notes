# Spring Boot 6일차 (수)

날짜: 2025년 6월 18일

# `Mustache 문법 사용`

mustache 에 중괄호 {{ }} 로 감싸서 변수를 출력

변수를 사용할 때 중괄호 2개를 사용한 다음, 그 안에 변수명을 넣어주면 됨.

spring Controller 에서 전달한 데이터를 페이지로 불러올 때 사용

helloworld() 안에다 Model model 추가

import 를 안했기에 오류 남…

우리가 사용하는 모델은 org.spring.framework 에 위치함

이거를 import 해야함.

```java
package com.example.project.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

// 1. Controller 어노테이션은 Controller임을 선언한다.
@Controller
public class MvcController {
    // 2. GetMapping 안에 url정의
    @GetMapping("/hello")
    // 3. 반환형 String인 helloWorld메서드 정의
    public String helloWorld(Model model) {
        // 4. 메서드에서 반환될 mustache 파일명을 리턴에 정의
        model.addAttribute("username", "Leo");
        return "hi";
    }
    @GetMapping("/bye")
    public String byeWorld(Model model) {
        // 모델을 사용하기 위한 모델 추가
        model.addAttribute("username1", "Micheal");
        return "bye";
    }

}
```

// Leo 라는 값을 가진 데이터를 등록함.

모델에서 변수를 등록함. 왼쪽에는 변수명, 오른쪽에는 값

이렇게 선언하면 hi.mustache 에서 username 이라는 변수를 사용할 수 있게함.

지금까지 구현 정리

1. hi.mustache → 2. MvcController → 3. helloworld() 

→ 4. 변수 만들기(username) 5. Controller → model 사용, model.addAttribute 모델에다가 변수 설정 → 6. 페이지 실행