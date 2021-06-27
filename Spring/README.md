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

- DAO(Data Access Object)
  - DB의 데이터를 조회하거나 조작하는 기능을 전담하도록 만든 객체를 말한다.
  - DB에 접근을 하기위한 로직과 비즈니스 로직을 분리하기 위해서 사용한다.
- DTO(Data Transfer Object)
  - 계층간 데이터 교환을 위한 자바빈즈를 말한다.
    - 여기서 말하는 계층 -> Controller, View, Business Layer, Persistent Layer
  - 일반적인 DTO 는 로직을 갖고 있지 않는 순수한 데이터 객체이며, 속성과 그 속성에 접근하기 위한 getter, setter 메소드만 가진 클래스이다.
  - VO(value Object) 라고도 불린다.
    - DTO와 달리 readOnly 속성을 가진다.
  
## AOP 란?
- **AOP(Aspect Oriented Programming)란**
  - Aspect Oriented Programming, 관점 지향 프로그래밍
  - 어떤 로직을 기준으로 핵심 관점과 부가 관점을 나누고, 관점을 기준으로 모듈화하는 것
  - 핵심 관점은 주로 핵심 비즈니스 로직
  - 부가 관점은 핵심 로직을 실행하기 위한 데이터베이스 연결, 로깅, 파일 입출력 등

## 필터(Filter)와 인터셉터(Interceptor) 차이
- 필터와 인터셉터?
  - 애플리케이션에서 자주 사용되는 기능(공통 부분) 을 분리하여 관리할 수 있도록 Spring이 제공하는 기능
  ![filter](https://github.com/WeareSoft/tech-interview/raw/master/contents/images/filterInterceptor.jpg)
1. 서버 실행 시 Servlet 이 올라오는 동안 init 후 doFilter 실행
2. Dispatcher Servlet을 지나쳐 Interceptor의 preHandler 실행
3. 컨트롤러를 거쳐 내부 로직 수행 후, Interceptor의 postHandler 실행
4. doFilter 실행
5. Servlet 종료 시 destroy

- **Filter 특징**
- Dispatcher Servlet 이전에 수행되고, 응답 처리에 대해서도 변경 및 조작 수행 가능
  - WAS 내의 ApplicationContext에서 등록된 필터가 실행
- WAS 구동 시 FilterMap이라는 배열에 등록되고, 실행 시 Filter chain을 구성하여 순차적으로 실행
- Spring Context 외부에 존재하여 Spring과 무관한 자원에 대해 동작
- 일반적으로 web.xml에 설정
- 예외 발생 시 Web Application에서 예외 처리
- ex. 인코딩 변환, XSS 방어 등
- 실행 메소드
  - init() : 필터 인스턴스 초기화
  - doFilter() : 실제 처리 로직
  - destroy() : 필터 인스턴스 종료
  
- **Interceptor 특징**
- Dispatcher Servlet 이후 Controller 호출 전, 후에 끼어들어 기능 수행
- Spring Context 내부에서 Controller의 요청과 응답에 관여하며 모든 Bean에 접근 가능
- 일반적으로 servlet-context.xml에 설정
- 예외 발생 시 @ControllerAdvice에서 @ExceptionHandler를 사용해 예외 처리
- ex. 로그인 체크, 권한 체크, 로그 확인 등
- 실행 메소드
  - preHandler() : Controller 실행 전
  - postHandler() : Controller 실행 후
  - afterCompletion() : view Rendering 후

#### Filter, Inerceptor 차이점 요약
- Filter는 WAS단에 설정되어 Spring과 무관한 자원에 대해 동작하고, Interceptor는 Spring Context 내부에 설정되어 컨트롤러 접근 전, 후에 가로채서 기능 동작
- Filter는 doFilter() 메소드만 있지만, Interceptor는 pre와 post로 명확하게 분리
- Interceptor의 경우 AOP 흉내 가능
  - handlerMethod(@RequestMapping을 사용해 매핑 된 @Controller의 메소드)를 파라미터로 제공하여 메소드 시그니처 등 추가 정보를 파악해 로직 실행 여부 판단 가능
