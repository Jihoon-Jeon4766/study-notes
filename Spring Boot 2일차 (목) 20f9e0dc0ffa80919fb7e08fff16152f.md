# Spring Boot 2일차 (목)

날짜: 2025년 6월 12일

![스크린샷 2025-06-12 11.03.22.png](Spring%20Boot%202%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2020f9e0dc0ffa80919fb7e08fff16152f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-12_11.03.22.png)

## 환경변수 JAVA_HOME 설정(zsh기준)

  1.zshrc 파일 열기

**nano ~/.zshrc**

1. 맨 아래에 다음 내용 추가

**export JAVA_HOME=”/Libary/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home”**

**export PATH =”$JAVA_HOME/bin:$PATH”**

1. 저장하고 나가기

**Ctrl + O (저장)**

**Enter (확인)**

**Ctrl + X (나가기)**

1. 변경 내용 적용

**source ~/.zshrc**

## 적용 확인

아래 명령어로 환경변수가 잘 설정 되었는지 확인:

**echo $/JAVA_HOME**

**java -version**

## 예시 출력

java version "17.0.15" 2025-04-15 LTS
Java(TM) SE Runtime Environment (build 17.0.15+9-LTS-241)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.15+9-LTS-241, mixed mode, sharing)

![스크린샷 2025-06-17 18.01.21.png](Spring%20Boot%202%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2020f9e0dc0ffa80919fb7e08fff16152f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-17_18.01.21.png)

![스크린샷 2025-06-12 11.38.07.png](Spring%20Boot%202%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2020f9e0dc0ffa80919fb7e08fff16152f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-12_11.38.07.png)

![스크린샷 2025-06-12 11.38.20.png](Spring%20Boot%202%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2020f9e0dc0ffa80919fb7e08fff16152f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-12_11.38.20.png)

# `Spring Framework`

스프링 프레임워크

자바 기반의 대표적인 프레임워크로, 객체 생성과 관리, 트랜잭션, AOP, MVC 웹 구조 등을 지원해, 엔터프라이즈급 웹 애플리케이션을 구성할 수 있게 해주는 강력한 기능을 제공.

# `Spring boot`

스프링 부트

스프링 프레임워크의 복잡한 설정을 최소화해주는 도구로, 자동설정, 내장 톰캣, 간편한 실행을 지원해서 빠르게 웹 프로젝트를 시작하고 배포할 수 있음.

# `part1. DI`

dependence - 의존성

**한 객체가 다른 객체의 기능이다 데이터를 사용할 때 생기는 관계**

A Class

```java
xxx(){
	B b = new B();
	b.method();
}
```

B Class

```java
method(){
	***
}
```

A는 B에 의존한다.

# `*// 객체 생성 시 인터페이스 사용하는 경우*`

```java
List list = new ArrayList();
```

- `List`는 인터페이스,  `ArrayList`는 구현체
- 이렇게 하면 나중에 `LinkedList`, `Vector` 등으로 구현체를 쉽게 바꿀 수 있다.
- 코드의 **유연성**과 **확장성**이 높아진다.

```java
ArrayList arrayList = new ArrayList();
```

- 이렇게 하면 `arrayList`는 오직 `ArrayList`만 사용할 수 있다.
- 추후 다른 리스트 구현체로 바꾸기 어렵다,
- 특정 구현에 **의존적**이므로 **유지보수가 불편**할 수 있다.

# `DI(Dependency Injection)`

## 의존성 주입

**객체가 직접 필요한 의존 객체를 생성하지 않고, 외부(프레임 워크 등)에서 필요한 객체를  주입받는 방식**.

```java
import org.springframework.stereotype.Component;

@Component
public class MyService {
    // 이 클래스는 스프링이 자동으로 객체 생성함 
}
```

`@Component`**는 Spring Framework에서 해당 클래스를 스프링이 자동으로 객체로 생성(빈 등록) 하게 해주는 어노테이션입니다.**

**먼저** 

`@Autowired`**는 Spring Framework에서 의존성 주입(Dependency Injection) 을 자동으로 해주는 어노테이션입니다.**

**설계 변경에 대응하기 위해 인터페이스를 이용해 의존성을 만들고, DI를 사용하여 사용되는 객체 클래스를 변경하는 경우, 사용하는 클래스를 수정없이 사용 가능**

# `EveningGreet 클래스`

```java
package com.example.project.basic.basic3;

import org.springframework.stereotype.Component;

@Component
public class EveningGreet implements Greet {
    @Override
    public void greeting() {
        System.out.println("-------------");
        System.out.println("좋은 저녁 입니다.");
        System.out.println("-------------");
    }
}
```

**@Component 어노테이션이 부여되어 EveningGreet 클래스의 인스턴스가 생성됨.**

# `ProjectApplication`

```java
package com.example.project;

import com.example.project.basic.basic3.Greet;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class ProjectApplication {

	public static void main(String[] args) {

		SpringApplication.run(ProjectApplication.class, args)
				.getBean(ProjectApplication.class).execute1();
	}

	@Autowired
	Greet greet;

	private void execute1() {
		greet.greeting(); //메서드 호출.
	}
}

```

**@Autowired 어노테이션에 따라 EveningGreet 클래스의 인스턴스가 클래스의 greet 필드에 주입되어 실행되면 greeting() 메서드가 실행됨..**

```java
package com.example.project.basic.basic3;

public interface Greet {
    //greeting 이라는 메서드를 만듬.
    void greeting();
}
```

# `Part2. AOP`

## AOP(Aspect Oriented Programming)

### 관점 지향 프로그래밍

**AOP는 공통적으로 사용되는 기능(로깅, 트랜잭션, 보안 등)을 핵심 비즈니스 로직과 분리하여, 관심사의 분리를 실현하는 프로그래밍 기법.**

# `build.gradle`

```java
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
	implementation 'org.springframework.boot:spring-boot-starter-mustache'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	implementation 'org.springframework.boot:spring-boot-starter-aop'

	runtimeOnly 'com.h2database:h2'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
	testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
}
```

# `basic4.SampleAspect 클래스`

```java
package com.example.project.basic.basic4;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.springframework.stereotype.Component;

import java.text.SimpleDateFormat;

@Aspect
@Component
public class SampleAspect {

    @Before("execution(* com.example.project.basic.basic3.*Greet.*(..))")
    public void beforeAdvice(JoinPoint joinPoint){
        System.out.println("======== Before Advice =========");

        System.out.println(new SimpleDateFormat("yyyy/MM/dd").format(new java.util.Date()));
        System.out.println(String.format("메서드: %s", joinPoint.getSignature().getName()));
    }
}
```

![스크린샷 2025-06-12 17.07.06.png](Spring%20Boot%202%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2020f9e0dc0ffa80919fb7e08fff16152f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-12_17.07.06.png)

중심적 관심사가 실행되기 전 Before Advice(횡단적 관심사 구현 메서드 : 어드바이스)가 실행된 것을 확인해봄.

```java
package com.example.project.basic.basic4;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.springframework.stereotype.Component;

import java.text.SimpleDateFormat;

@Aspect
@Component
public class SampleAspect {

    @After("execution(* com.example.project.basic.basic3.*Greet.*(..))")
    public void afterAdvice(JoinPoint joinPoint){
        System.out.println("======== After Advice ========");
        System.out.println(new SimpleDateFormat("yyyy/MM/dd").format(new java.util.Date()));
        System.out.println(String.format("메서드 : %s", joinPoint.getSignature().getName()));
    }
}

```

![스크린샷 2025-06-12 17.23.31.png](Spring%20Boot%202%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8E%E1%85%A1%20(%E1%84%86%E1%85%A9%E1%86%A8)%2020f9e0dc0ffa80919fb7e08fff16152f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2025-06-12_17.23.31.png)