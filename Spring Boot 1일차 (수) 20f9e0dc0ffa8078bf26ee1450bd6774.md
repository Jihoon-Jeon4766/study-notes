# Spring Boot 1일차 (수)

날짜: 2025년 6월 11일

# `Framework`

### 프레임워크

## Frame + work

“틀” + “일하다”의 합성어

합쳐서 “틀을 가지고 일하다”

프라 모델 키트 부품 = “Framework”

다양한 건담 = “page”

# `Framework`

일정한 구조나 규칙에 따라 코드를 작성할 수 있도록 도와주는 재사용 가능한 소프트웨어 툴로 개발 효율성을 높이고, 일 관련된 구조를 유지하게 해줌

# `Library`

프로그램을개발하기 위해 사용되는 도구 모음

# `Framework 와 Library 차이점`

---

Framework           차이점

규악, 틀 제공           자유도

---

Library                 공통점

도구 모음               프로그램을 쉽게 만들기 위한 것

---

# `Spring Boot`

복잡한 설정이 빠르게 웹 어플리케이션을 개발할 수 있도록 도와주는 Spring 프레임워크 기반의 개발 도구

# `환경구성`

## JDK(Java Development Kit)

JDK는 자바 개발 키트의 약자로 개발자들이 Java 기반 소프트웨어를 개발하기 위한 도구 모음

## IDE(Integrated Development Environment)

코드를 작성하고, 저장하고 컴파일 및 디버깅을 도와주는 통합 개발 환경으로 자바 개발자의 필수 프로그램

# `IDE download`

[https://www.jetbrains.com/idea/download/?section=mac](https://www.jetbrains.com/idea/download/?section=mac)

![스크린샷 2025-06-11 18.28.10.png](Spring%20Boot%201%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%2020f9e0dc0ffa8078bf26ee1450bd6774/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-11_18.28.10.png)

# `Spring Project 만들기`

[https://start.spring.io/](https://start.spring.io/)

![스크린샷 2025-06-11 20.27.57.png](Spring%20Boot%201%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%2020f9e0dc0ffa8078bf26ee1450bd6774/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-11_20.27.57.png)

# `의존성 4가지 추가`

**Spring Web**

**Mustache -html 템플릿 엔진** 

**Spring Data JPA - DB를 저장하거나 데이터 조회를 자동화**

**H2 Database - 가벼운 인메모리 데이터**

![스크린샷 2025-06-11 21.04.01.png](Spring%20Boot%201%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%89%E1%85%AE)%2020f9e0dc0ffa8078bf26ee1450bd6774/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-11_21.04.01.png)

# `Project`

**Project : 전체 프로젝트가 저장되는 최상위 디렉터리**

**Java : 애플리케이션의 핵심 기능을 작성하는 JAVA 파일들의 위치**

**Resources : 외부 파일 (설정파일, 정적파일, 템플릿)을 담음**

**Project Application : Spring Boot 애플리케이션을 시작하는 진입점 -tomcat**

**Build.gradle : 프로젝트 빌드 방식 및 의존성 관리하는 설정 파일**