# (JPA)Entity VS VO VS DTO
## DTO(Data Transfer Object)
계층간 데이터 교환을 위한 객체(Java Beans)이다. Layer간의 통신용도로 오가는 객체를 말한다. DTO는 일반적으로 말하는 객체라고는 볼 수 없다. 단순히 데이터를 담는 곳으로 구조체라고 볼 수 있다.

## Entity
실제 DB의 테이블과 매칭될 클래스이다. 즉, 테이블과 링크될 클래스임을 나타낸다. 단, Domain Logic만 가지고 있어야 하고 Presentation Logic을 가지고 있어서는 안된다. 여기서 구현한 method는 주로 Service Layer에서 사용한다.

## VO(Value Object)
VO는 DTO와 동일한 개념이지만 read only 속성을 갖는다.(불변 객체) VO는 특정한 **비즈니스** 값을 담는 객체이고, DTO는 Layer간의 통신 용도로 오고가는 객체를 말한다. 따라서 VO는 비즈니스 로직을 가질 수 있다.
