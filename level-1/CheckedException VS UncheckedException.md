# CheckedException VS UncheckedException
## CheckedException
CheckedException은 **반드시 처리해야하는** 예외로서, 컴파일 시점에 판단된다. 이는 `RuntimeException`을 상속하지 않은 예외들을 말한다. CheckedException가 발생할 수 있는 메서드를 사용하는 경우, **복구가 가능한 예외들이므로 반드시 예외를 처리해야 하는 코드를 함께 작성해야한다.** `try/catch`문으로 예외를 잡아서 처리하던지, `throws`로 예외를 자신이 호출한 곳으로 던지는 방법으로 해결할 수 있다. 이를 해결하지 않으면 컴파일 에러가 발생한다.

## UncheckedException
UncheckedException는 런타임 시점에 판단되는 예외로서, 처리하지 않는다고 해서 컴파일 에러가 발생하지는 않는다. 프로그래머의 실수, 잘못 만 든 code, core(기본)적인 문제 등으로 인해 발생하는 예외이다.

|  | Checked Exception | Unchecked Exception |
|------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------|
| 처리 여부 | 반드시 예외 처리 해야함 | 예외 처리 하지 않아도됨 |
| 트랜잭션 Rollback 여부 | Rollback 안됨, 해결할 수 있으므로 롤백하거나 처리하거나 선택지를 준다.(개발자가 try/catch로 해야하므로) | Rollback 진행, 해결할 수 없으므로 롤백한다. |
| 대표 Exception | IOException, SQLException | NullPointException, IllgerArgumentException |

## 참고 자료
- http://www.nextree.co.kr/p3239/
