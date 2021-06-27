# Spring
🔖 Contents

- [스프링 프레임 워크란?](#스프링-프레임-워크란?)
- [Spring Bean 이란?](#Spring-Bean-이란?)
- [IoC 란?](#IoC-란?)
- [DI 란?](#DI-란?)
- [POJO](#POJO)
- [DAO 와 DTO 의 차이](#DAO-와-DTO-의-차이)
- [AOP 란?](#AOP-란?)
- [필터(Filter)와 인터셉터(Interceptor) 차이](#필터(Filter)와-인터셉터(Interceptor)-차이)

<hr>

## 스프링 프레임 워크란?

자바 플랫폼을 위한 오픈소스 애플리케이션 프레임워크로서 엔터프라이즈급 애플리케이션을 개발하기 위한 모든 기능을 종합적으로 제공하는 경량화된 솔루션이다.
- 동적인 웹사이트를 개발하기 위한 여러 가지 서비스를 제공한다.
 
- **특징**
    - 스프링은 경량 컨테이너로 자바 객체를 담고 직접 관리한다. 객체의 생성 및 소멸 그리그 라이프 사이클을 관리하며 언제든 Spring 컨테이너로 부터 필요한 객체를 가져와 사용할 수 있다. 이는 Spring 이 [IoC](#IoC-란?) 기반의 Framework 임을 의미한다.

## Spring Bean 이란?

- `Spring IoC Container` 가 관리하는 자바 객체,`Spring Bean Container` 안에 들어있는 객체
- 컨테이너에 담겨있으며, 필요할 때 컨테이너에서 가져와서 사용
- @Bean 을 사용하거나 xml 설정을 통해 일반 객체를 Bean으로 등록할 수 있고, Bean으로 등록된 객체는 쉽게 주입하여 사용 가능

#### Bean 의 생명주기
- 객체생성 -> 의존 설정 -> 초기화 -> 사용 -> 소멸
- 스프링 컨테이너에 의해 생명주기 관리
- 스프링 컨테이너 초기화 시 빈 객체 생성, 의존 객체 주입 및 초기화
- 스프링 컨테이너 종료 시 빈 객체 소멸

#### Bean 등록하는 방법
1. @Component 어노테이션 사용(Component Scan 을 통한 등록)
- @Controller,@Service,@Entity 등도 클래스 파일을 열어보면 내부적으로 @Component 어노테이션을 사용한다.
2. 빈 설정파일(xml)에 직접 등록

#### Bean 초기화 및 소멸 방법
1. InitializingBean, DisposableBean InterFace 구현을 통한 초기화/소멸
```java
public interface InitializingBean {
    void afterPropertiesSet() throws Exception;
}

public interface DisposableBean {
    void destroy() throws Exception;
}

```

```java
@Component
class Person implements InitializingBean, DisposableBean {
   private int age;

   public Person(int age) {
      this.age = age;
   }

   @Override
   public void destroy() throws Exception {
      System.out.println("hello destroy");
   }

   @Override
   public void afterPropertiesSet() throws Exception {
      System.out.println("hello initialize");
   }
}

```

2. PostConstructor, preDestroy 어노테이션을 통한 초기화/소멸

```java
@Component
class Person {
   private int age;

   public Person(int age) {
      this.age = age;
   }

   @PostConstruct
   public void init() {

   }

   @PreDestroy
   public void destroy() {

   }
}
```
## IoC 란?

`IoC(Inversion of Control)` 란 "제어의 역전" 이라는 의미로, 말 그대로 메소드나 객체의 호출작업을 개발자가 결정하는 것이 아니라, 외부에서결정되는 것을 의미한다.
객체의 의존성을 역전시켜 객체 간의 결합도를 줄이고 유연한 코드를 작성할 수 있게 하여 가독성 및 코드 중복, 유지 보수를 편하게 할 수 있게 한다.

- Spring에서의 IoC
  - Spring 프레임워크에서 지원하는 ioc Container는 우리들이 흔히 개발하고 사용해왔던 일반 `POJO` 의 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능들을 제공한다.
- 라이브러리와 프레임워크의 차이
  - IoC의 개념이 적용되었나의 차이
  - 라이브러리를 사용하는 애플리케이션 코드는 애플리케이션 흐름을 직접 제어한다. 단지 동작하는 중에필요한 기능이 있을 때 능동적으로 라이브러리를 사용할 뿐이다.
  - 반면에 프레임워크는 거꾸로 애플리케이션 코드가 프레임워크에 의해 사용된다. 보통 프레임워크 위에 개발한 클래스를 등록해두고, 프레임워크가 흐름을 주도하는 중에 개발자가 만든 애플리케이션 코드를 사용핟도록 만드는 방식이다.

기존에 객체가 만들어지고 실행되는 순서
1. 객체 생성
2. 의존성 객체 생성(클래스 내부에서 생성)
3. 의존성 객체 메소드 호출

스프링에서 객체가 만들어지고 실행되는 순서
1. 객체 생성
2. 의존성 객체 주입(스프링이 만들어놓은 객체(Bean) 을 주입)
3. 의존성 객체 메소드 호출(@Autowired 등)

## DI 란?

#### DI(Dependency Injection)
`DI(Dependency Injection)`란 스프링이 다른 프레임워크와 차별화되어 제공하는 의존 관계 주입 기능으로, 객체를 직접 생성하는 게 아니라 외부에서 생성한 후 주입 시켜주는 방식이다.
DI를 통해서 모듈 간의 결합도가 낮아지고 유연성이 높아진다.

![img-di](https://media.vlpt.us/images/gillog/post/08489bda-549e-4dae-851b-8ae1734bf85e/21373937580AEF9B37.jpg)
*출처 : https://velog.io/@gillog/Spring-DIDependency-Injection*

첫번째 방법은 A객체가 B와 C객체를 New 생성자를 통해서 직접 생성하는 방법이고,

두번째 방법은 외부에서 생성 된 객체를 setter()나 생성자를 통해 사용하는 방법이다.

이러한 두번째 방식이 의존성 주입의 예시인데,
A 객체에서 B, C객체를 사용(의존)할 때 A 객체에서 직접 생성 하는 것이 아니라 외부(IOC컨테이너)에서 생성된 B, C객체를 조립(주입)시켜 setter 혹은 생성자를 통해 사용하는 방식이다.

![img-di2](https://media.vlpt.us/images/gillog/post/41f2eb24-fce2-4b7e-b9ac-d5c3ce97d213/22535642580C4AF12C.jpg)
*출처 : https://velog.io/@gillog/Spring-DIDependency-Injection*

스프링에서는 객체를 [Bean](Spring-Bean-이란?)이라고 부르며, 프로젝트가 실행될때 사용자가 [Bean](Spring-Bean-이란?) 관리하는 객체들의 생성과 소멸에 관련된 작업을 자동적으로 수행해주는데 객체가 생성되는 곳을 스프링에서는 Bean 컨테이너라고 부른다.

## POJO

- **POJO(Plain Old Java Object)란?**
  - 프레임워크 인터페이스나 클래스를 구현하거나 확장하지 않는 단순한 클래스.
- 왜 POJO를 지향해야 하는가?
  - 스프링 이전에 원하는 엔터프라이즈 기술이 있다면 그 기술들을 직접적으로 사용하는 개체를 설계했는데, 특정 기술과 환경에 종속되어 의존하게 된 자바 코드는 가독성이 떨어져 유지보수에 어려움이 있고. 또한, 특정 기술의 클래스를 상속받거나, 직접 의존하게 되어 확장성이 매우 떨어지는 단점이 있었다. 이는 즉, 대표적인 객체지향 언어인 자바가 객체지향 설계의 장점들을 잃어버리게 된 것이다.
- 특징
  - Java 에서 제공하는 API 외에 종속되지 않음
  - 특정 규약, 환경에 종속되지 않음
- 환경에 종속되지 않는 것의 장점
  - 코드가 간결해짐
  - 비즈니스 로직과 특정 환경이 분리되므로 단순함
  - 자동화 테스트에 유리(환경 종속적인 코드는 자동화 테스트가 어렵지만, POJO는 테스트가 매우 유연)
  - 객체지향 설계의 자유로운 사용

## DAO 와 DTO 의 차이
## AOP 란?
## 필터(Filter)와 인터셉터(Interceptor) 차이
