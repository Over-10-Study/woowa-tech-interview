# new String() vs ""(문자열 리터럴)
`new`를 통해 `String`을 생성하면 Heap 영역에 존재하게 되고 리터럴을 이용할 경우 string constant pool이라는 영역에 존재하게 된다. Java6까지 string constant pool의 위치는 Perm 영역이었다. Perm 영역에 위치하였던 게 Java7에서 Heap 영역으로 변경되었다. 그 이유는 OutOfMemory 문제 때문이다.

문자열 리터럴을 사용하면 내부적으로 `String`의 `intern()` 메서드를 호출한다. 그리고 이 메서드는 string constant pool에 현재 생성할 문자열과 같은 문자열이 있는지 검사한 후 있다면 기존에 존재하는 문자열 객체를 반환하고(주소값이 동일), 없다면 새로 만든다.

Perm 영역은 런타임 시간에는 고정 크기로 사용된다.(컴파일 시간에는 크기를 조정할 수 있다.) 이러한 이유 때문에 문자열 리터럴을 만들 때 `String`의 `intern()`를 호출하는데 이는 고정된 Perm 사이즈 때문에 OutOfMemory 문제가 발생할 수 있었다. 그래서 Java7 부터 string constant pool 위치를 Heap 영역으로 옮기게 되었다. 이는 OutOfMemory 문제를 해결했을 뿐 아니라 GC의 대상이 되므로, 문자열 리터럴을 메모리 해제시켜줄 수 있게 되었다.

```java
@Test
void stringTest() {
    String str1 = "abc";
    String str2 = "abc";
    String str3 = new String("abc");
    String str4 = new String("abc").intern();

    assertThat(str1 == str2).isTrue();
    assertThat("abc" == "abc").isTrue();
    assertThat(stringReturn() == "abc").isTrue();
    assertThat(stringReturn() == str1).isTrue();
    assertThat(STRING_TEST == str1).isTrue();
    assertThat(str3 == str1).isFalse();
    assertThat(str4 == str1).isTrue();
}

String stringReturn() {
    return "abc";
}
```
