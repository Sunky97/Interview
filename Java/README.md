# Java
🔖 Contents

- [Java 와 C 의 차이점](#Java-와-C-의-차이점)
- [Java 언어의 장단점](#Java-언어의-장단점)
- [접근제어자의 종류와 특징](#접근제어자의-종류와-특징)
- [primitive Type 과 reference Type](#primitive-Type-과-reference-Type)
- [Wrapper Class](#Wrapper-Class)
- [String, StringBuilder, StringBuffer 의 차이?](#String,-StringBuilder,-StringBuffer-의-차이?)
- [OOP 의 정의와 4가지 특징](#OOP-의-정의와-4가지-특징)
- [OOP 의 5대 원칙](#OOP-의-5대-원칙)
- [객체지향 프로그래밍과 절차지향 프로그래밍의 차이](#객체지향-프로그래밍과-절차지향-프로그래밍의-차이)
- [JVM](#JVM)
- [추상클래스](#추상클래스)
- [인터페이스](#인터페이스)
- [인터페이스와 추상 클래스의 차이](#인터페이스와-추상-클래스의-차이)
- [클래스, 객체, 인스턴스 차이](#클래스,-객체,-인스턴스-차이)
- [다형성이란?](#다형성이란?)
- [배열과 컬렉션의 차이](#배열과-컬렉션의-차이)
- [Annotation](#Annotation)
- [오버로딩(Overloading)과 오버라이딩(Overriding)](#오버로딩(Overloading)과-오버라이딩(Overriding))
- [Java COllection Framework](#Java-Cllection-Framework)
- [제네릭(Generic)](#제네릭(Generic))
- ['==' 와 'equals()' 의 차이](#'=='-와-'equals()'-의-차이)
- [자바에서 멀티스레드 구현방법](#자바에서-멀티스레드-구현방법)
- [Stream 이란?](#Stream-이란?)
- [Lambda란?](#Lambda란?)
- [동기화와 비동기화](#동기화와-비동기화)
- [리플렉션(Reflection)](#리플렉션(Reflection))
- [GC 란?](#GC-란?)
- [GC 의 장점](#GC-의-장점)

<hr>

## Java 와 C 의 차이점
1. c 는 절차지향언어, Java 는 객체지향언어
2. c 는 메모리를 직접 조절가능, Java 는 GC 가 자동으로 메모리 관리
3. c 의 처리속도가 상대적으로 빠름

## Java 언어의 장단점
- 장점
  - 자바는 JVM 을 통해 동작하기 때문에, 운영체제에 독립적이다.
  - 객체지향언어이다.
  - 자동으로 메모리 관리를 해준다.
  - 멀티스레드를 쉽게 구현할 수 있다.
- 단점
  - 비교적 속도가 느리다.
  - 프로그램 발생 시 발생할 수 있는 예외들을 개발자가 직접 처리해야한다. 그렇지 않으면 컴파일이 되지않음.

## 접근제어자의 종류와 특징
|접근제어자|설명|
|---|---|
|public|접근 제한이 없다.|
|protected|같은 패키지 내에서, 그리고 다른 패키지의 자손클래스에서 접근이 가능하다.|
|default|같은 패키지 내에서만 접근이 가능하다.|
|private|같은 클래스 내에서만 접근이 가능하다.|

## primitive Type 과 reference Type
1. 기본 데이터 타입(Primitive Data Type)
 - 변수에 값 자체를 저장한다.
 - byte, short, char, int, float, double, boolean 이 있다.
 - 기본 타입의 크기가 작고 고정적이기 때문에 메모리의 Stack 영역에 저장된다.
2. 참조형 데이터 타입(Reference Data Type)
 - 메모리상에 객체가 있는 위치를 저장한다.
 - 기본 데이터 타입을 제외한 모든 타입이 참조형 데이터 타입이다.
 - 참조 타입의 데이터의 크기가 가변적, 동적이기 때문에 동적으로 관리되는 Heap 영역에 저장된다.
 - 더 이상 참조하는 변수가 없을 때 가비지 컬렉션에 의해 파괴된다.

## Wrapper Class
기본형 데이터 타입으로 표현할 수 있는 간단한 데이터를 객체로 만들어야 할 경우가 있는데 그러한 기능을 지원하는 클래스를 뜻한다.
|기본형|Wrapper Class|
|---|---|
|byte|Byte|
|short|Short|
|int|Integer|
|long|Long|
|char|Character|
|float|Float|
|double|Double|
|boolean|Boolean|

## String, StringBuilder, StringBuffer 의 차이?
- 공통점
  - 세가지 모두 String(문자열)을 저장하고 관리하는 클래스
- 차이점
  - String 객체는 **불변** 하기때문에 '+' 연산이나 .concat() 메소드를 이용해서 문자열 값에 변화를 줘도 값 자체가 변하는 것이 아니라, 새로 메모리를 할당받아 String 클래스 객체를 만들어서 문자열을 나타낸다.
  - StringBuilder 와 StringBuffer 는 기존 객체의 공간이 부족하게 되는 경우 기존의 버퍼 크기를 늘리며 유연하게 동작한다.(가변적)

**StringBuilder**
- Thread-safe 하지 않음
- StringBuffer 보다 성능이 좋음

**StringBuffer**
- Thread-safe 함(동기화 지원)

### 정리
- 성능 : StringBuilder > StringBuffer > String
- String : 문자열 연산이 적고 멀티쓰레드 환경일 경우
- StringBuffer : 문자열 연산이 많고 멀티쓰레드 환경일 경우
- StringBuilder : 문자열 연산이 많고 단일쓰레드이거나 동기화를 고려하지 않아도 되는 경우  

## OOP 의 정의와 4가지 특징

#### 정의
OOP 란? 현실 세계를 프로그래밍으로 옮겨와 프로그래밍하는 것을 말한다. 현실 세계의 사물들을 객체라고 보고 그 객체로부터 개발하고자 하는 애플리케이션에 필요한 특징들을 뽑아와 프로그래밍 하는 것이다.

#### 특징

1. 추상화(Abstraction)
    - 구체적인 정보는 무시하고 필요성에 의해 있어야할 정보들만 간추려서 구성하는 것
2. 캡슐화(Encapsulation)
    - 높은 응집도, 낮은 결합도를 유지하여 유연함과 유지보수성 증가
    - 필요가 없는 정보는 외부에서 접근하지 못하도록 제한하는 것
3. 상속(Inheritance)
    - 여러 개체들이 가진 공통된 특성을 부각시켜 하나의 개념이나 법칙으로 성립시키는 과정
4. 다형성(Polymorphism)
    - 서로 다른 클래스의 객체가 같은 메시지를 받았을 때 각자의 방식으로 동작하는 능력
    - 오버라이딩(Overriding), 오버로딩(Overloading)
  
## OOP 의 5대 원칙

"SOLID" 원칙
- S: 단일 책임 원칙(SRP, Single Responsibility Principle)
    - 객체는 단 하나의 책임만 가져야 한다.
- O: 개방-폐쇄 원칙(OCP,Open Closed Principle)
    - 확장에는 열려있으나 변경에는 닫혀 있어야 한다.
- L: 리스코프 치환 원칙(LSP, Liskov Substitution Principle)
    - 자식클래스는 최소한 자신의 부모 클래스에서 가능한 행위는 수행할 수 있어야 한다.
- I: 인터페이스 분리 원칙(ISP, Interface Segregation Principle)
    - 한 클래스는 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다. 하나의 일반적인 인터페이스보다는, 여러 개의 구체적인 인터페이스가 낫다.
- D: 의존 역전 원칙(DIP, Dependency Inversion Principle)
    - 의존 관계를 맺을 때, 변화하기 쉬운것 보단 변화하기 어려운 것에 의존해야 한다.

## 객체지향 프로그래밍과 절차지향 프로그래밍의 차이
## JVM
## 추상클래스
## 인터페이스
## 인터페이스와 추상 클래스의 차이
## 클래스, 객체, 인스턴스 차이
## 다형성이란?
## 배열과 컬렉션의 차이
## Annotation
## 오버로딩(Overloading)과 오버라이딩(Overriding)
## Java COllection Framework
## 제네릭(Generic)
## '==' 와 'equals()' 의 차이
## 자바에서 멀티스레드 구현방법
## Stream 이란?
## Lambda란?
## 동기화와 비동기화
## 리플렉션(Reflection)
## GC 란?
## GC 의 장점
