# Spring
🔖 Contents

- [스프링 프레임 워크란?](#스프링-프레임-워크란?)
- [Bean 이란?](#Bean-이란?)
- [IOC 란?](#IOC-란?)
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
    - 스프링은 경량 컨테이너로 자바 객체를 담고 직접 관리한다. 객체의 생성 및 소멸 그리그 라이프 사이클을 관리하며 언제든 Spring 컨테이너로 부터 필요한 객체를 가져와 사용할 수 있다. 이는 Spring 이 [IOC](#IOC-란?) 기반의 Framework 임을 의미한다.

## Bean 이란?

- `Spring IoC Containe`r 가 관리하는 자바 객체,`Spring Bean Container` 안에 들어있는 객체
- 컨테이너에 담겨있으며, 필요할 때 컨테이너에서 가져와서 사용
- @Bean 을 사용하거나 xml 설정을 통해 일반 객체를 Bean으로 등록할 수 있고, Bean으로 등록된 객체는 쉽게 주입하여 사용 가능

#### Bean 의 생명주기
- 객체생성 -> 의존 설정 -> 초기화 -> 사용 -> 소멸
- 스프링 컨테이너에 의해 생명주기 관리
- 스프링 컨테이너 초기화 시 빈 객체 생성, 의존 객체 주입 및 초기화
- 스프링 컨테이너 종료 시 빈 객체 소멸

#### Bean 초기화 방법 3가지
1. 빈 초기화 메소드에 `@PostConstruct` 사용
    - 빈 정의 xml 에 `<context:annotation-config></context:annotation-config>` 추가
2. `InitializingBean` 인터페이스의 `afterPropertiesSet()` 메소드 오버라이드
3. 커스텀 init() 메소드 정의
    - 빈 정의 xml 에 `init-method` 속성으로 메소드 이름 지정
    - 또는 빈 초기화 메소드에 `@Bean(init-method="init")` 지정

#### Bean 소멸 방법 3가지
1. 빈 소멸 메소드에 `@PreDestory` 사용

## IOC 란?

## DI 란?
## POJO
## DAO 와 DTO 의 차이
## AOP 란?
## 필터(Filter)와 인터셉터(Interceptor) 차이
