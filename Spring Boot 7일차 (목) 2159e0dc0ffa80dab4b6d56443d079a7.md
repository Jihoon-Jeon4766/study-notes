# Spring Boot 7일차 (목)

날짜: 2025년 6월 19일

# `Board(게시판)`

## create

1. 입력 폼 만들기(boards/new.mustache)

templates → boards 패키지 생성

boards → new.mustache 파일 생성

1. 코드 작성

```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Document</title>
</head>
<body>
{{>layout/header}}

    <form action = ""> // 1. 입력 폼
        <input type = "text"> // 2. 게시판 제목 입력
        <textarea> // 3. 게시판의 내용 입력
        </textarea>
        <button type = "submit"> Submit </button> // 4. 버튼 생성
    </form>

{{>layout/footer}}
</body>
</html>
```

1. 컨트롤러 만들기

controller → [BoardsController.java](http://BoardsController.java) 파일생성.

1. 코드 작성

```java
package com.example.project.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class BoardsController {
    @GetMapping("/boards/new")
    public String newBoardForm(){
        return "boards/new";
    }
}
```

1. 실행

[local.host](http://localhost:8080/boards/new):8080/boards/new

![스크린샷 2025-06-19 11.51.52.png](Spring%20Boot%207%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%202159e0dc0ffa80dab4b6d56443d079a7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-19_11.51.52.png)

1. 해결#1  (hi.mustache → header.mustache)

```java
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">

    <title>Hello, world!</title>
</head>

<body>

<!--navigation-->
<nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                <li class="nav-item">
                    <a class="nav-link active" aria-current="page" href="#">Home</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Link</a>
                </li>
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                        Dropdown
                    </a>
                    <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                        <li><a class="dropdown-item" href="#">Action</a></li>
                        <li><a class="dropdown-item" href="#">Another action</a></li>
                        <li><hr class="dropdown-divider"></li>
                        <li><a class="dropdown-item" href="#">Something else here</a></li>
                    </ul>
                </li>
                <li class="nav-item">
                    <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
                </li>
            </ul>
            <form class="d-flex">
                <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
                <button class="btn btn-outline-success" type="submit">Search</button>
            </form>
        </div>
    </div>
</nav>
```

<!— navigation —> 위에 붙여넣기

부트스트랩 디자인 적용을 하기 위해 항상 필요한 설정코드를  header.mustache에 추가.

![스크린샷 2025-06-19 11.46.10.png](Spring%20Boot%207%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%202159e0dc0ffa80dab4b6d56443d079a7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-19_11.46.10.png)

해결#2 (hi.mustache → footer.mustache)

```java
<!--site info-->
<div class="mb-5 containeer-fluid">
    <hr>

    <p>⚔️SpringBootStuding | <a href = '#'>Privacy</a> | <a href="#">Terms</a></p>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>

</body>
</html>
```

1. 코드 복사

Bootstrap → FORMS → OverView → code copy

→ boards/new.mustache

![스크린샷 2025-06-19 12.28.04.png](Spring%20Boot%207%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%202159e0dc0ffa80dab4b6d56443d079a7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-19_12.28.04.png)

1. new.mustche (처음에 했던 form 코드 삭제 )

```java
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Document</title>
</head>
<body>
{{>layout/header}}

<form>
    <div class="mb-3">
        <label class="form-label"> 제목 </label>
        <input type="text" class="form-control">
        <div id="emailHelp" class="form-text"> 제목을 한글로만 작성해주세요 </div>
    </div>
    <div class="mb-3">
        <label class="form-label"> 내용 </label>
        <textarea class = "form-control" rows ="3"></textarea>
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>

</form>

{{>layout/footer}}
</body>
</html>
```

1. 추가  Submit → create.mustache 이동하게끔

```java
<form class = "container" action ="/boards/create" method = "post">
```

1. DTO 만들기 (dto/BoardForm.java)

1. 코드작성

```java
package com.example.project.dto;

public class BoardForm {
    private String title;
    private String content;

    public BoardForm(String title, String content) {
        this.title = title;
        this.content = content;
    }

    @Override
    public String toString() {
        return "BoardForm{" +
                "title='" + title + '\'' +
                ", content='" + content + '\'' +
                '}';
    }

}
```

titile, content → Genertate..  → Constructort 

                                            → toString()

1. 코드작성

```java
@PostMapping("/boards/create")
    public String createBoard(BoardForm boardform){
        System.out.println(boardform.toString());
        return "boards/create";
    }
```

`Controller`에서 form 데이터를 받을 때 `DTO`에 담아오기 때문에 `DTO`를 생성한다.

form 데이터에서 toString() 이 반환되었는지 출력

1. 코드작성

```java
<form class = "container" action ="/boards/create" method = "post">
    <div class="mb-3">
        <label class="form-label"> 제목 </label>
        <input type="text" class="form-control" name = "title">

    </div>
    <div class="mb-3">
        <label class="form-label"> 내용 </label>
        <textarea class = "form-control" rows ="3" name = "content"></textarea>
        <div id="emailHelp" class="form-text"> 성적인 내용을 담은 욕설이나 비하, 음란한 표현을 하지 마세요 </div>
    </div>
```

name= “title, content” 이렇게 추가

이유 "해당 데이터를 전달 객체인 DTO에 선언한 이유는, 클라이언트로부터 전달받은 값을 일시적으로 담기 위해서입니다. 이후 이 값을 서비스 계층이나 DB에 저장하기 위해 사용합니다.”