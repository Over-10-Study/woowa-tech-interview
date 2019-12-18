# Enum(열거형)
Enum은 열거형(enumerated type)이라고 부른다. 열거형은 서로 연관된 상수들의 집합이라고 할 수 있다.

## Enum의 특징
- 문자열과 비교하여, IDE의 적극적인 지원을 받을 수 있다.
- 자동완성, 오타 검증, 텍스트 리팩토링 등 허용 가능한 값들을 제한할 수 있다.
- 리팩토링시 변경 범위가 최소화 된다. 내용의 추가가 필요하더라도, enum 코드 외에는 수정할 필요가 없다.

## Java만의 enum 특징
Java의 enum은 위의 다른 언어의 enum보다 더 많은 장점을 갖고 있다. 대표적으로 C/C++의 enum의 경우 결국은 int값만으로 사용할 수 있지만, Java에서는 완전한 기능을 갖춘 클래스로 사용할 수 있다.

### Java Enum 참고 자료
- http://woowabros.github.io/tools/2017/07/10/java-enum-uses.html
