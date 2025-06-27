# Spring Boot 10일차 (화)

날짜: 2025년 6월 24일

# `DTO를 데이터 베이스에 저장하기`

DB는 SQL문만 이해 가능

### 엔티티(Entity): 자바 객체를 DB가 이해할 수 있도록 만든 것으로, 이를 기반으로 테이블이 생성됨

### 라파지터리(rapository) : 엔티티가 DB 속 테이블에 저장 및 관리 될 수 있게 하는 인터페이스

![스크린샷 2025-06-24 16.57.49.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_16.57.49.png)

1. create class Board 

![스크린샷 2025-06-24 17.00.47.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_17.00.47.png)

1. entity 파일에 Board 만듬

→ 어노테이션 @Entity

![스크린샷 2025-06-24 17.05.18.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_17.05.18.png)

1. @id → 기본키 지정

![스크린샷 2025-06-24 17.09.06.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_17.09.06.png)

1. 자동으로 값이 생성되는 필드 → 그게 id

![스크린샷 2025-06-24 17.10.01.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_17.10.01.png)

1. @Column → 필드 선언

**엔티티 클래스의 필드를 데이터베이스 테이블의 컬럼에 매핑**할 때 사용됩니다.

![스크린샷 2025-06-24 17.13.10.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_17.13.10.png)

이걸 기반으로 테이블이 생성된다. (JPA)

DTO → 엔티티 → table - id / title / content

```java
package com.example.project.entity;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.Id;

@Entity
public class Board {

    @Id
    @GeneratedValue
    private Long id;

    @Column
    private String title;

    @Column
    private String content;

    public Board(Long id, String title, String content) {
        this.id = id;
        this.title = title;
        this.content = content;
    }

    @Override
    public String toString() {
        return "Board{" +
                "id:" + id +  "title: " + title + "content:" + content;
    }

}
```

1. create method toEntitiy 

DTO인 form 객체를 Entity 객체로 변환해줍니다.

![스크린샷 2025-06-24 17.57.23.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_17.57.23.png)

1. form 데이터를 다음 DTO 객체를 entity로 반환한다.

```java
public Board toEntity() {
        return new Board(null,title,content);
    }
```

# `라파지터리`

1. 리파지터리로 엔티티 DB에 저장

→ Create pakage→ `repository`

![스크린샷 2025-06-24 18.15.08.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_18.15.08.png)

1. 인터페이스 →  `BoardRepository`

![스크린샷 2025-06-24 18.22.13.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_18.22.13.png)

```java
package com.example.project.repository;

import com.example.project.entity.Board;
import org.springframework.data.repository.CrudRepository;

public interface BoardRepository extends CrudRepository<Board, Long> {

}
```

# `CrudRepository 생성, 조회, 추가, 삭제`

Board : 관리 대상 클래스 타입이고

Long : 관리대상 엔티티에 아이디 값

```java
spring.h2.console.enabled=true
```

h2 DB를 웹 접근 콜솔로 허용

![스크린샷 2025-06-24 20.44.57.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_20.44.57.png)

[http://localhost:8080/h2-console](http://localhost:8080/h2-console/login.jsp?jsessionid=1b7062a598f777ee191315f7685fbbcf)

![스크린샷 2025-06-24 20.46.15.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_20.46.15.png)

URL 에 → jdbc:h2:mem:085d41ca-ec95-4dbc-a323-e32436972f86

→ conect

![스크린샷 2025-06-24 20.53.39.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_20.53.39.png)

![스크린샷 2025-06-24 20.55.18.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_20.55.18.png)

![스크린샷 2025-06-24 20.55.01.png](Spring%20Boot%2010%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%92%E1%85%AA)%2021c9e0dc0ffa80b09936ea6d60eeb146/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-24_20.55.01.png)