# Encapsulation(캡슐화)

> hide one part of the system from another part of the system.
> in so doing we prevent one possible place where we might do unforeseen harm
> -Emergent Design (https://play.google.com/store/books/details?id=Q_3i19icWKMC&pcampaignid=books_web_aboutlink)

한 번 만들고 끝나는 프로그램이 아니라면 지속적으로 변경되는 요구사항에 따라 계속 코드를 변경해야한다. 그러면 코드를 수정할 때 가장 두려운 것은 변경한 부분으로 인해 다른 곳에 영향이 미치는 것이다. 따라서 영향을 주지 않기 위해 이러한 부분들을 숨겨야한다. 이를 캡슐화라고 부른다.

캡슐화는 객체지향프로그래밍 뿐 아니라 컴퓨터의 전반적인 부분에 적용되는 개념이다. 캡슐화로 숨겨서 보이지 않으면 그 부분은 다른 곳에서 접근조차 할 수 없다.

## 객체지향 프로그래밍에서 캡슐화
### 클래스
- 접근 제어자
  - private : 자기 클래스 내부의 메서드에서만 접근 허용
  - protected : 자기 클래스 내부 또는 상속받은 자식 클래스에서 접근 허용
  - public : 모든 접근을 허용한다.
- 메서드
  - 내가 요청하는 방식을 제한한다.(파라미터와 리턴 값이 정해져있다.)
  - 예를 들어, 메서드 내부에서 지역변수를 가지고 있다면 이는 무엇을 하든 외부에서 전혀 알 수 없다. 외부의 코드는 해당 지역변수에 영향을 절대 미칠 수 없다.
- 디자인 패턴
  - Strategy Pattern: 어떤 구현체를 선택할지 숨긴다.
  - Decorator Pattern: 어떤 순서로 적용할지 숨긴다.
