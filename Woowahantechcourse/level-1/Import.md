# Import
Import는 다른 패키지에 있는 클래스를 사용하는 방법이다. 다른 패키지에 있는 클래스를 사용할 때 항상 접두사로 패키지명을 사용하는 것은 매우 귀찮은 작업이고, 가독성도 떨어뜨린다. 이를 해결해주는 것이 import문이다. import문을 사용하려면 해당 패키지를 알고 있어야 한다. (특히 다른 모듈이면, 의존성 주입이 필요하다.)

추가적으로 자바에서 Import의 특징은 다음과 같다.
- 자바는 기본이 되는 클래스라 대부분의 클래스에서 자주 사용하는 클래스를 java.lang에서 자동으로 import한다.
- 대표적으로 String, Integer와 같은 클래스는 import 없이 사용할 수 있다.
- 바로 앞의 Input 예제에서 System도 클래스인데 import를 하지 않아도 사용 가능한 이유는 java.lang.System에 존재하기 때문에 자동으로 import된 것이다.
- Static import는 클래스안에 있는 static member를 사용한다.
