# StringBuilder VS StringBuffer
`StringBuilder`와 `StringBuffer` 둘 다 자바에서 String(문자열)을 저장하고 관리하는 클래스이다. `String` 클래스와 차이점은 `String` 클래스는 **불변** 이고, `StringBuilder`와 `StringBuffer`는 **가변*** 이라는 점이다. 따라서 이 두 클래스는 문자열 연산이 많은 환경에서 `String`보다 효율적으로 사용할 수 있다.

`String` 클래스는 불변객체이므로 문자열 연산을 하면 기존의 객체에 추가하는 것이 아닌 새로운 객체를 메모리에 할당한다. 따라서 문자열 연산이 많을 경우 `String` 클래스를 사용 시 **메모리 할당 및 제거가 자주 일어나므로 성능에 좋지않다.**

## `StringBuilder`
- 동기화가 되지 않기 때문에 싱글쓰레드, 쓰레드를 신경쓰지 않아도 되는 곳에서 사용 가능하다.
- 단일 쓰레드 환경에선 StringBuilder가 더 성능이 좋다.

## `StringBuffer`
- 가변객체로써 문자열 연산이 많은 환경에서 사용할 수있다.
- 동기화를 지원하기 때문에 멀티쓰레드 환경에서 사용할 수 있다. (synchronized)

## `StringBuilder` VS `StringBuffer`
- 같은 메소드를 사용할 수 있다.
- jdk 1.5부터 String의 + 도 StringBuilder로 컴파일되게 변경했지만, String 객체를 생성하는건 동일하기 때문에 Builder 사용을 권장.
