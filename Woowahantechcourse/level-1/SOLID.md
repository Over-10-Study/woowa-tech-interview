# SOLID

|첫글자|약어|개념|상세|
| --- | ---- | ------------------------ | ------------------------------------------------------- |
S|	SRP	| 단일 책임 원칙 (Single responsibility principle) | 한 클래스는 하나의 책임만 가져야 한다.
O|	OCP	| 개방-폐쇄 원칙 (Open/closed principle) | “소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.”
L|	LSP	| 리스코프 치환 원칙 (Liskov substitution principle) |“프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.” 계약에 의한 설계를 참고하라.
I|	ISP	| 인터페이스 분리 원칙 (Interface segregation principle)|“특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.”
D|	DIP	|의존관계 역전 원칙 (Dependency inversion principle)|프로그래머는 “추상화에 의존해야지, 구체화에 의존하면 안된다.” 의존성 주입은 이 원칙을 따르는 방법 중 하나다.

## 원칙(Principle) 이란?
특정 상황에 대한 정답이라기보다는 좋은 또는 나쁜 코드에 대한 기준을 좀 더 구체적으로 표현한다고 볼 수 있다.

## SRP (Single Responsibility Principle)
SRP는 높은 cohesion(응집도)로 만들며, 이는 변경될 이유가 동일한 것들끼리 잘 모아놓은 것을 말한다.

> Responsibility == "A reason for change"

객체가 하나의 책임만 가진다면, 변경할 이유도 단 하나여야 한다. 만약 여러가지 책임이 있다면 해당 책임들이 서로 의존할 수 있다. 이는 모듈과 같은 자기에게 필요하지 않는 것들이 있을 수도 있음을 의미한다.

### 적용될 경우 좋은점
- 각 패키지, 클래스, 메서드가 변경될 이유가 단 한가지가 된다. 해당 기능을 구현한 클래스를 찾기 쉽다.
- 테스트하기 쉬운 코드가 된다.


## OCP (Open-Closed Principle)
OCP는 확장에는 열려있고, 변경에는 닫혀있는 것을 말한다. 즉, 요구사항이 변경되었을 때, 기존의 코드의 수정 없이 새로운 기능이 추가될 수 있어야 한다.

> 어떻게 가능한가요? 답은 추상화..!

- 존재하는 인터페이스에서는 코드 수정이 있으면 안됨(변경에 닫힘)
- 새로운 기능을 인터페이스를 구현함으로 만족시키기(확장에 열린)

> 'The existing interface is closed to modifications and new implementations must, at a minimum, implement that interface.'


## LSP (Liskov Substitution Principle)
LSP는 S가 T의 sub type 일 경우 (더 구체적인 값), T가 사용된 곳을 S로 대체해도 아무 문제 없어야 한다.
- 기존에 T를 생각하고 했던 가정들이 S에 대해서도 아무 문제 없어야 함
    - ex. 직사각형, 정사각형 문제
        - setWidth 는 사실은 2개의 가정이 있음 (모서리에 인접한 두 변을 a, b라 하자. a 가 width 인 경우)
            - a 를 바꿈
            - b 는 바뀌면 안됨
- 그렇기 때문에 S로 형변환하거나 `instanceOf S` 등으로 S에 대해 특별한 처리를 하면 좋지 않다고 하는 것
    - S에 대한 특별한 처리가 필요하다는 것이 T를 완전히 대체하지 못한다는 것이기에


## ISP (Interface Segregation Principle)
한 클래스는 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다는 원리이다. 사용자 입장에서 사용하지 않는 메서드가 있을 때 다른 인터페이스로 분리해야 한다. ISP는 하나의 일반적인 인터페이스보다는 여러 개의 구체적인 인터페이스가 낫다고 본다. 그리고 SRP가 클래스의 단일책임을 강조한다면 ISP는 인터페이스의 단일책임을 강조한다고 볼 수 있다.

> 'the interfaces of the class can be broken up into groups of member functions.'

## DIP (Dependency Inversion Principle)
결국 사용하는 애든, 사용당하는 애든, 추상화(interface)를 의존하고 있어야 한다. (사진보면 이해가 그나마 쉽다.)

<wiki 그림>

> 'Nevertheless, the "inversion" concept does not mean that lower-level layers depend on higher-level layers. Both layers should depend on abstractions that draw the behavior needed by higher-level layers.'

## 참고
- https://sites.google.com/site/unclebobconsultingllc/getting-a-solid-start
- http://www.nextree.co.kr/p6960/
