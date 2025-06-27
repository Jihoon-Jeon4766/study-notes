# Spring Boot 12일차 (목)

날짜: 2025년 6월 26일

# `게시판 (Read)`

## `조회 과정`

1. URL 요청 등록 
2. 요청 받은 id 값 확인
3. 데이터 조회
4. 모델 데이터 등록
5. view 페이지 반환
6. view 페이지 → 모델 등록 코드 작성 & 출력

# `1.→ BoardsController`

```java
@GetMapping("/boards/{id}")
    public String read(@PathVariable Long id){
        log.info("id :" +id);
        return "boards/read";
    }
```

[http://localhost:8080/boards/1](http://localhost:8080/boards/1) →pk → id

[http://localhost:8080/boards/2](http://localhost:8080/boards/2) → pk → id

[http://localhost:8080/boards/3](http://localhost:8080/boards/3) → pk → id

id 라는 변수를 선언 했다.

Controller에서도 ID라는 프라이머리키가 필요하다.

@PathVariable → URL에 있는 id를 가져오기 위해 매개변수로 id를 받아 올 수 있다.

![스크린샷 2025-06-26 10.51.52.png](Spring%20Boot%2012%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2021e9e0dc0ffa806db25cf38aa431710c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-26_10.51.52.png)

# `2.데이터를 조회하기..`

2.1 id를 조회해서 데이터를 가져오기

```java
//1. id를 조회해서 데이터를 가져오기
        Board boardEntity = boardRepository.findById(id);
```

findById → JPA의 Repository라는 메서드가 있다.

Entity로 반환해준다.

type이 달라서 형 변환을 해줘야함 

→ Optional type miss math

![스크린샷 2025-06-26 11.04.09.png](Spring%20Boot%2012%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2021e9e0dc0ffa806db25cf38aa431710c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-26_11.04.09.png)

# `#빨간줄 해결`

![스크린샷 2025-06-26 11.07.18.png](Spring%20Boot%2012%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2021e9e0dc0ffa806db25cf38aa431710c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-26_11.07.18.png)

```java
.orElse(null);
```

1. type 문제 해결
2. 데이터를 찾을 때 해당 id 값이 없으면 null 값으로 반환해줌.

2.2 모델에 데이터 저장

```java
//2. 모델에 데이터 등록하기
        model.addAttribute("board",boardEntity);
```

`→ submit` 

![스크린샷 2025-06-26 12.01.13.png](Spring%20Boot%2012%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2021e9e0dc0ffa806db25cf38aa431710c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-26_12.01.13.png)

**`boards/1` 이유: 기본 생성자가 없어서** 

![스크린샷 2025-06-26 12.02.39.png](Spring%20Boot%2012%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2021e9e0dc0ffa806db25cf38aa431710c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-26_12.02.39.png)

# `→Entity → Board`

기본 생성자가 없어서 
`@NoArgsConstructor` 추가 오류 해결!!

![스크린샷 2025-06-26 12.18.37.png](Spring%20Boot%2012%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2021e9e0dc0ffa806db25cf38aa431710c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-26_12.18.37.png)

# `read.mustache`

```java
{{>layout/header}}

<table class="table">
    <thead>
    <tr>
        <td> id</td>
        <td> title</td>
        <td> content</td>
    </tr>
    </thead>
    
    {{#board}}
    <tbody>
        <tr>
            <td> {{id}} </td>
            <td> {{title}}</td>
            <td> {{content}}</td>
        </tr>
    {{/board}}
    </tbody>

</table>

{{>layout/footer}}
```

![스크린샷 2025-06-26 12.25.16.png](Spring%20Boot%2012%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2021e9e0dc0ffa806db25cf38aa431710c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-26_12.25.16.png)

![스크린샷 2025-06-26 12.26.30.png](Spring%20Boot%2012%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2021e9e0dc0ffa806db25cf38aa431710c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-26_12.26.30.png)

==================================================

# `전체 목록 조회 하기`

```java
//전체 조회 메서드
    @GetMapping("boards")
    public String reads(){

	     return "";
    }
```

1. 모든 데이터 가져오기

```java
//1. 모든 데이터 가져오기
        List<Board> boardEntityList = boardRepository.findAll();
                
        
```

![스크린샷 2025-06-26 12.51.34.png](Spring%20Boot%2012%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2021e9e0dc0ffa806db25cf38aa431710c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-26_12.51.34.png)

형 변환 바꿔주기

→ `BoardRepository`

```java
package com.example.project.repository;

import com.example.project.entity.Board;
import org.springframework.data.repository.CrudRepository;

import java.util.ArrayList;

public interface BoardRepository extends CrudRepository < Board, Long > {

    @Override
    ArrayList<Board> findAll();

}
```

1. 모델 데이터 등록하기

```java
//2. 모델에 데이터 등록하기
        model.addAttribute("boardEntityList",boardEntityList);
```

1. 뷰 페이지 반환하기

```java
//3. 뷰 페이지 반환하기
        return "boards/reads";
```

# `reads.mustache 만들기`