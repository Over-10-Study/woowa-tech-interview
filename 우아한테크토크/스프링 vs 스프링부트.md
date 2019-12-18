# Spring vs Spring Boot

> Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".
> Spring Boot를 사용하면 "실행"할 수있는 독립형 프로덕션 급 Spring 기반 응용 프로그램을 쉽게 만들 수 있습니다.

Spring Boot는 Spring에 비해 크게 두 가지 장점이 있다.
- **내장 서버(Embedded Tomcat)** 를 가지고 있다.
  - 서버가 내장되어있어 `war` 파일이 아닌 `jar` 파일로도 단독 배포가 가능하다.
  - 기본적으로 톰캣이 내장되어 있지만 gradle에서 jetty 등 다른 것으로 변경할 수 있다.
- **의존성 관리** 가 편하다.
  - `starter` 지원: 변경 요소가 크기 않는 많은 설정들을 기본적으로 지원한다.(보일러 플레이트, 수정없이 계속 재사용 가능)
  - `starter` 사용 시 자동으로 권장 버전을 알려주기 때문에 호환성을 고려하지 않아도 된다.
  - Java 코드에서 설정하던 것들도 `application.properties` 또는 `application.yml` 로 관리할 수 있다.

## 참고 자료
- https://www.youtube.com/watch?v=6h9qmKWK6Io&list=PLgXGHBqgT2TvpJ_p9L_yZKPifgdBOzdVH&index=15
- https://jojoldu.tistory.com/43
