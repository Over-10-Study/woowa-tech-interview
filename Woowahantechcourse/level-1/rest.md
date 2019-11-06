# REST(REpresentational State Transfer)
REST는 위키백과의 정의에 따르면 다음과 같다.

> a way of providing interoperability between computer systems on the internet
> - Wikipedia -

- `interoperability`: 상호운영성

하지만 이렇게만 봐서는 정확히 어떤 의미인지 알기 힘들다. 먼저 REST의 역사를 살펴보면서 어떻게 REST가 만들어졌는지부터 REST라는 것이 정확히 무엇인지 알아보자.

## REST 역사
1991년 WEB이 나왔다. 여기서 어떻게 인터넷에서 정보를 공유할 지가 문제였다. 이를 해결하는 방법으로 모든 정보를 하이퍼텍스트로 연결했다.
- 표현 형식: HTML
- 식별자: URI
- 전송 방법: HTTP

데이터를 표현하는 방법은 HTML 형식으로 했으며, 이를 식별하기 위한 방법으로 URI를 사용했다. 그리고 이러한 정보를 통신하는 방법이 HTTP였다.

### HTTP/1.0(1994-1996)

> Roy T. Fielding: How do i improve HTTP without breaking the Web?

HTTP/1.0이 나오기 이전부터 HTTP는 Web에서 전송 방법으로 사용하고 있었고, 전세계에는 수 많은 Web 서버가 존재하고 있었다. 이 시점에서 로이 필딩은 HTTP 명세를 만들고 기능을 추가하는 작업을 해야 했다. 로이 필딩은 만약 HTTP를 변경한다면 기존의 HTTP를 사용하던 Web에 영향이 미칠 것으로 생각했다. 이를 해결하기 위해 만든 것이 HTTP Object Model 이었다. 그리고 이것이 4년 후 1998년 REST라는 이름으로 발표되고, 바로 2년 후 로이 필딩의 박사 논문으로 제출된다.

### API
인터넷이 발전하면서 API 역시 급속도로 생겨나기 시작했다. 그 중 Microsoft는 원격에서 메서드를 호출할 수 있는 [XML-RPC(1998)](https://ko.wikipedia.org/wiki/XML-RPC)을 만든다. 이는 후에 SOAP이라는 이름으로 바뀐다. 그리고 2000년 2월 Salesforce는 SOAP을 이용하여 최초로 인터넷에 Salesforce API를 공개한다.

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:enterprise.soap.sforce.com" xmlns:urn1="urn:sobject.enterprise.soap.sforce.com" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <soapenv:Header>
    <urn:SessionHeader>
      <urn:sessionId>[sessionId retrieved from the login() call]</urn:sessionId>
    </urn:SessionHeader>
  </soapenv:Header>
  <soapenv:Body>
    <urn:create>
      <urn:sObjects xsi:type="urn1:Account">
        <Name>Sample Inbound Account One</Name>
      </urn:sObjects>
    </urn:create>
  </soapenv:Body>
</soapenv:Envelope>
```

위 예제는 Salesforce API의 모습이며, 이는 매우 복잡하다. 4년 후 2004년 8월 Flickr API가 나왔고 이는 SOAP과 REST를 사용한 두 가지 API를 만들었다. 아래는 그 예제이다.

- SOAP

```xml
<s:Envelope
	xmlns:s="http://www.w3.org/2003/05/soap-envelope"
	xmlns:xsi="http://www.w3.org/1999/XMLSchema-instance"
	xmlns:xsd="http://www.w3.org/1999/XMLSchema"
>
	<s:Body>
		<x:FlickrRequest xmlns:x="urn:flickr">
			<method>flickr.test.echo</method>
			<name>value</name>
		</x:FlickrRequest>
	</s:Body>
</s:Envelope>
```

- REST

```
https://www.flickr.com/services/rest/?method=flickr.test.echo&name=value
```

위는 같은 기능을 하는 Flickr API를 SOAP과 REST 두 형식으로 나타낸 것이다. 한 눈에 봐도 REST가 훨씬 간단해보인다. SOAP는 REST에 비해 복잡하고, 규칙이 많고, 어려워 보인다. 그에 반해 REST는 단순해보인다. 그 결과 REST는 빠른 속도로 발전하게 되었고 다음과 같은 결과를 만들었다.
- 2006년, AWS는 자사 API 사용량의 85%가 REST임을 밝혔다.
- 2010년, Salesforce.com은 REST API를 추가하였다.

### Microsoft REST API Guidelines(2016)
- URI는 `http://{serviceRoot}/{collection}/{id}` 형식이어야 한다.
- GET, PUT, DELETE, POST, HEAD, PATCH, OPTIONS를 지원해야한다.
- API 버저닝은 Major.minor로 하고 URI에 버전 정보를 포함시킨다.
- 등등...

위는 마이크로소프트에서 만든 REST API 가이드라인이다. 이를 본 로이 필딩은 해당 가이드라인은 REST API가 아닌 HTTP API라고 해야한다고 말했다. 그리고 REST API를 위한 최고의 버저닝 전략은 버져닝 자체를 하지 않는 것이라고 덧붙였다. 그렇다면 무엇이 문제인 것일까?


## REST API
REST API는 **REST 아키텍처 스타일을 따르는 API** 를 말한다.
- **REST**: 분산 하이퍼미디어 시스템(예:웹)을 위한 아키텍쳐 스타일
- **아키텍쳐 스타일**: 제약조건의 집합

따라서 REST 제약조건을 모두 만족한 API가 REST API이다.


## REST를 구성하는 제약조건
### Client-Server 구조
Server는 자원을 가지고 있고, client는 자원을 요청하는 입장이다.
- REST Server: API를 제공하고, 비즈니스 로직 처리 및 저장을 담당한다.
- Client: 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.

이처럼 서버와 클라이언트 각각의 역할이 명확히 구분되므로 서로간의 의존성이 줄어들게 된다.

### Stateless(무상태)
REST의 가장 큰 특징 중 하나는 HTTP 웹 표준을 그대로 사용하고 있다. 따라서 HTTP가 stateless protocol이므로, REST 역시 stateless 특징을 갖고 있다. 무상태는 서버에서 클라이언트의 세션과 쿠기와 같은 context를 저장하지 않으므로 구현이 단순해진다. 그리고 서버는 각각의 요청을 완전히 독립된 요청으로 인식하고 처리할 수 있으므로 처리 방식에 일관성을 부여하고 부담이 적으며, 서비스의 자유도가 높아진다.

### Cache(캐시 처리 가능)
REST는 HTTP 웹 표준을 사용하므로 기존 웹에서 사용하는 인프라를 그대로 사용할 수 있다. 따라서 HTTP가 가진 캐시 처리 기능이 적용가능하다. HTTP 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다. 캐시 사용으로 많은 양의 요청을 효율적으로 처리할 수 있고 응답 시간이 빨라지는 등 서버의 자원을 효율적으로 사용할 수 있다.

### Layered System(계층화)
REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있다. 또한 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수도 있다.

### Code-On-Demand(optional)
Conde-On-Demand는 REST 서버에서 클라이언트로 코드를 보낸 후 클라이언트는 이 코드를 수행할 수 있어야 한다. 이 코드는 현재 대부분 사용하고 있는 javascript를 말한다. Conde-On-Demand는 반드시 충족할 필요는 없다.

### Uniform Interface(인터페이스 일관성)
Uniform Interface는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 말한다. 즉, 통일된 Interface를 통해 어떠한 기술(Python, PHP, C#, Ruby, Java)이든 플랫폼(iOS, Android, Mac, Windows)이든 상관없이 사용할 수 있다. REST를 구성하는 제약조건 중 Uniform Interface 제외한 조건들은 대부분 HTTP 특징과 거의 동일하기 때문에 개발자가 신경쓰지 않아도 충분히 잘 지킬 수 있다. 하지만 Uniform Interface는 아키텍쳐 스타일로서 여러 제약조건이 있는데, 대부분 이를 지키지 못한다. 그래서 위에서 살펴봤듯이, REST가 아니라는 말이 계속 나오고 있고 이는 현재도 마찬가지이다.


## Uniform Interface의 제약조건
- Identification of resources: 리소스가 URI로 식별된다.
- Manipulation of resources through representations: 리소스를 삭제하거나 수정할 때 HTTP 메시지에 이러한 표현을 담아서 전송해야한다.
- **Self-Descriptive Messages**
- **Hypermedia As The Engine Of Application State(HATEOAS)**

위의 네 가지 조건 중에서 대부분 지켜지지 않는 것은 아래의 두 가지 조건이다. 거의 대부분 API가 이 두 조건을 지키지 못하고 있다.

### Self-Descriptive Messages
Self-Descriptive Messages는 서버와 클라이언트 사이에서 주고 받는 **메시지는 스스로를 설명해야한다는 의미이다.** 이 말은 메시지만 보고도 어떤 기능을 수행하는지 알 수 있어야 한다는 것이다. 아래의 예제를 보자.

```
GET / HTTP/1.1
```

이 요청 메시지는 목적지가 빠져있어 Self-Descriptive Messages 조건을 만족하지 못한다. 이를 만족하려면 아래와 같이 목적지 링크를 담고 있어야 한다.

```
GET / HTTP/1.1
Host: www.example.org
```

다음은 응답 메시지이다.

```
HTTP/1.1 200 OK

[ {op: "remove", path: "a/b/c" } ]
```

이 응답 메시지는 본문에 JSON 형식의 데이터를 담고 있다. 하지만 클라이언트에서 이 메시지만 보고서는 해당 본문이 어떤 데이터 형식인지 알 수 없다.

```
HTTP/1.1 200 OK
Content-Type: application/json

[ {op: "remove", path: "a/b/c" } ]
```

위와 같이 내용의 타입을 선언해야한다. 그래야 아래 본문을 해석할 수 있다. 하지만 여기서도 Self-Descriptive Messages 조건을 만족하지 못한다. 왜냐하면 `op`, `path`가 어떤 의미인지 알 수 없기 때문이다.

```
HTTP/1.1 200 OK
Content-Type: application/json-patch+json

[ {op: "remove", path: "a/b/c" } ]
```

이를 해결하는 방법 역시 알맞은 Content-Type을 설정하는 것이다. 위 Content-Type의 명세를 찾아서 이를 해석해야 한다. Self-Descriptive Messages 조건은 메시지를 봤을 때 온전히 해석이 가능해야한다. 오늘날의 API는 단순히 JSON이라고만 적혀있어 메시지만 보고서는 완전히 해석할 수 없는 경우가 대부분이다.

### Hypermedia As The Engine Of Application State(HATEOAS)
HATEOAS는 애플리케이션의 상태는 Hyperlink를 이용해 전이되어야한다는 의미이다.

<애플리케이션 상태 전이 그림>

위 그림에서 `[]` 가 링크라고 생각하자. 따라서 페이지마다 이러한 링크를 클릭하면 다른 페이지로 이동하며, 이를 애플리케이션 상태가 전이된다고 말한다. 이 구현은 HTML로 되어 있으며 대부분의 HTML은 HATEOAS를 만족한다. 간단하게 HATEOAS를 만족하는 HTML 예제 코드를 보자.

```
HTTP/1.1 200 OK
Content-Type: text/html

<html>
<head></head>
<body><a herf="/test">test</a></body>
</html>
```

JSON도 HATEOAS를 만족시킬 수 있는 방법이 존재한다.

```
HTTP/1.1 200 OK
Content-Type: application/json
Link: </articles/1>; rel="previous",
      </articles/3>; rel="nest";

{
  "title": "The second article",
  "contents": "blah blah..."
}
```

위는 이전 페이지와 다음 페이지의 링크가 메시지를 통해 드러나 있고, Link는 JSON 표준에 등록되어 있다.


## 왜 API는 REST가 잘 안될까?
Web은 REST를 잘 적용했지만 API는 왜 되지 않을까? 그 이유에 대해 살펴보자.

|  | 흔한 웹 페이지 | HTTP API |
|:------------:|:--------------:|:---------:|
| Protocol | HTTP | HTTP |
| 커뮤니케이션 | 사람-기계 | 기계-기계 |
| Media Type | HTML | JSON |

위 표를 보면 웹 페이지와 HTTP API 사이에서는 미디어 타입만 다르다. 그러면 이 미디어 타입을 비교해보자.

|  | HTML | JSON |
|:----------------:|:-------------:|:------------------:|
| Hyperlink | 됨(a tag 등) | 정의되어 있지 않음 |
| Self-Descriptive | 됨(HTML 명세) | 불완전 |

Self-Descriptive가 불완전한 이유는 JSON이 파싱은 가능하지만 파싱된 안의 데이터는 해석할 수 없기 때문이다. 그래서 이를 위한 문서를 따로 만들어야한다.


## HTML과 JSON 메시지 비교
### HTML

```
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
Content-Type: text/html

<html>
<body>
<a href="https://todos/1">회사 가기</a>
<a href="https://todos/2">집에 가기</a>
</body>
</html>
```

- Self-Descriptive (만족)
  - 응답 메시지의 Content-Type을 보고 media type이 text/html임을 확인한다.
  - HTTP 명세에 media type은 IANA에 등록되어있다고 하므로, IANA에서 text/html 설명을 찾는다.
  - IANA에 따르면 text/html의 명세는 http://www.w3.org/TR/html 이므로 링크로 가서 명세를 해석한다.
  - 명세에 모든 테그의 설명이 있으므로 이를 참고하여 해석한다.
- HATEOAS (만족)
  -  a 태그로 표현된 링크를 통해 다음 상태로 전이할 수 있으므로 만족한다.

### JSON

```
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
Content-Type: application/json

[
  {"id": 1, "title": "회사 가기"},
  {"id": 2, "title": "집에 가기"}
]
```

- Self-Descriptive (불만족)
  - application/json도 text/html과 같은 과정으로 명세를 찾을 수 있다.
  - 명세를 통해 JSON을 파싱할 수는 있지만 **"id", "title"이 무엇인지는 알 수 없다.**
- HATEOAS (불만족)
  - 다음 상태로 전이할 링크 자체가 없다.


## JSON을 REST API로 고쳐보자.
### Self-Descriptive 만족시키기
- 방법 1: Media type을 등록한다.
  - 미디어 타입을 하나 정의한다.
  - 미디어 타입 문서를 작성하고 id, title에 대한 설명을 추가한다.
  - IANA에 등록한다.
  - 다른 사람이 이를 보고 해석할 수 있다.

```
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
Content-Type: application/vnd.todos+json

[
  {"id": 1, "title": "회사 가기"},
  {"id": 2, "title": "집에 가기"}
]
```

- 방법 2: Profile
  - "id", "title"이 무엇인지에 대한 명세를 작성한다.
  - Link 헤더에 profile relation으로 해당 명세를 링크한다.
  - 단점은 클라이언트가 Link 헤더(RFC 5988)와 profile(RFC 6906)을 알아야 한다.
  - 또 다른 단점은 Content negotiation을 할 수 없다.
    - 클라이언트가 지원하지 못하는 것을 서버가 알아챌 수 없다.(미디어 타입은 알 수 있다.)

```
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
Content-Type: application/json
Link: <https://example.org/docs/todos>; rel="profile"

[
  {"id": 1, "title": "회사 가기"},
  {"id": 2, "title": "집에 가기"}
]
```

### HATEOAS 만족시키기
단순히 링크를 추가하면 된다.

```
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
Content-Type: application/json
Link: <https://example.org/docs/todos>; rel="profile"

[
  {
    "link": "http://example.org/todos/1",
    "title": "회사 가기"
  },
  {
    "link": "http://example.org/todos/2",
    "title": "집에 가기"
  }
]
```

## Uniform Interface을 지켜야하는 이유
Uniform Interface가 필요한 이유는 독립적인 진화때문이다. 이는 서버와 클라이언트가 각각 독립적으로 진화한다는 뜻이다. 서버의 기능이 변경되더라도 예를 들어 API의 기능이 추가되거나 삭제되어도 클라이언트에게는 전혀 영향을 미치지 않는다는 것이다. 즉 클라이언트를 업데이트할 필요가 없다. 이러한 이유가 로이 필딩이 REST를 만든 이유이다.

웹에서는 Uniform Interface를 매우 잘지키고 있다. 이는 다음과 같은 이유가 있다.
- 웹 페이지를 변경했다고 해서 웹 브라우저를 업데이트할 필요는 없다.
- 웹 브라우저를 변경했다고 해서 웹 페이지를 업데이트할 필요는 없다.
- HTTP 명세가 변경되어도 웹은 잘 동작한다.
- HTML 명세가 변경되어도 웹은 잘 동작한다.

물론 이러한 변경때문에 웹 UI가 살짝 깨질 수는 있다. 하지만 최소한의 기능 동작은 한다. 하지만 모바일 앱은 웹과 다르다. 항상 업데이트가 필요하다. 심지어 서버가 변경되었을 때 클라이언트에서 필수적으로 변경되어야 하는 부분이 있어 강제로 업데이트를 시도할 때도 있다. 이러한 모바일 앱은 REST하지 않다고 볼 수 있다.

### Web은 어떻게 REST를 잘 지킬 수 있었을까?
간단히 말하면 수 많은 사람의 노력에 의해 지켜질 수 있었다. HTML5 초안에서 권고안이 나오는데 6년이 걸렸고, HTTP/1.1 명세 개정판을 작업하는데 7년이 걸렸다. 이만큼 노력하고 있다. 7년동안 기능이 하나도 추가안되고 문서만 변경했다. 이러한 노력은 **하위 호환성을 유지하기** 위함이다. 즉, 상호운영성(interoperability)을 지키기 위한 집착이다. 이러한 집착때문에 다음과 같은 일이 있었다.
- Referer 오타이지만 고치지 못했다. 이를 고치는 순간 웹이 깨지기 때문이다.
- charset 잘못 지은 이름이지만 고치지 못한다. 사실 인코딩이라는 이름으로 했어야 했다.
- HTTP 상태 코드 418 포기했다.(만우절 때 이상한 스팩을 만들었는데 이를 사용하는 웹이 있으므로 고치지 못했다, 영구 결번됨)
- HTTP/0.9를 현재까지도 지원한다.(크롬, 파이어폭스)
  - 크롬에서 이 버전을 빼다가 프록시에서 오동작이 발샘하여 포기하였다.

만약 이러한 노력이 없었다면 웹에서도 모바일 앱과 같이 다음과 같은 에러를 매우 자주 볼 수 있었을 것이다.

```
Netscape 6.0은 지원하지 않습니다.
```

### Self-Descriptive, HATEOAS가 독립적인 진화에 도움이 되는 이유
- Self-Descriptive
  - 확장 가능한 커뮤니케이션
  - 서버나 클라이언트가 변경되더라도 오고가는 메시지는 언제나 Self-Descriptive이므로 해석이 가능하다.
- HATEOAS
  - 애플리케이션 상태 전이의 late binding이다.
  - 어디서 어디로 가는지 미리 정해지지 않는다.
  - 어떤 상태로 전이가 완료되고 나서야 다음 전이 상태를 알 수 있다.(링크는 동적으로 변경될 수 있다.)
  - 서버가 링크를 마음대로 바꿔도 전혀 상관없다. 클라이언트는 그에 따라 전이만 되면 된다.


## 참고 자료
- https://www.youtube.com/watch?v=RP_f5dMoHFc&t=1060s
- https://slides.com/eungjun/rest#/
- https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html
- https://meetup.toast.com/posts/92
