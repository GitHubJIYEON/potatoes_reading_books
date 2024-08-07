## HTTP의 특성

HTTP 응용 계층에서 정보를 주고받는 데 사용되는 프로토콜
HTTP의 설계 목적은 확장성과 견고성

HTTP의 4가지 특성
요청-응답 기반 프로토콜

-   클라이언트-서버 구조 기반의 요청-응답 프로토콜
-   클라이언트는 서버에게 요청 메시지를 전송
-   서버는 클라이언트에게 요청에 대한 응답 메시지를 전송
-   HTTP메시지는 HTTP요청 메시지와 HTTP응답 메시지는 형태가 다름

미디어 독립적 프로토콜

-   클라이언트는 HTTP요청 메시지를 통해 서버의 자원을 요청할 수 있음
-   서버는 HTTP응답 메시지로 요청받은 자원에 대해 응답할 수 있음
-   (HTTP를 정의한 공식문서)RFC9110: HTTP가 요청하는 대상을 자원이라고 합니다. HTTP는 자원의 특성을 제한하지 않으며, 단지 자원과 상호 작용하는 데 사용할 수 있는 인터페이스를 정의할 뿐 대부분의 자원은 URI로 식별됩니다.

-   HTTP에서 메시지로 주고받는 자원의 종류 (MIME타입)
-   HTTP를 주고받을 미디어 타입에 특별히 제한을 두지 않고 독립적으로 동작이 가능한 미디어 독립적인 프로토콜이라고 할 수 있음
-   HTML, 일반 텍스트, PNG 이미지 타입을 나타냄
-   슬래시를 기준으로 타입/서브타입 형식으로 구성됨
-   타입은 데이터의 유형을 나타내고, 서브타입은 주어진 타입에 대한 세부 유형을 나타냄
-   별표문자(\*) 여러 미디어 타입을 통징하기 위해 사용됨
-   부가적인 설명을 위해 선택적으로 매개변수가 포함될 수 있음
-   매개변수는 ‘타입/서브타입;매개변수 = 값’의 형식으로 표현됨

스테이트리스 프로토콜

-   HTTP는 상태를 유지하지 않는 스테이트리스 프로토콜
-   서버가 HTTP요청을 보낸 클라이언트와 관련된 상태를 기억하지 않는다는 의미
-   클라이언트의 모든 HTTP요청은 기본적으로 독립적인 요청으로 간주됨
-   서버는 여러 대 구성이면 모든 클라이언트의 상태를 유지할 경우 클라이언트는 여러 서버를 동시에 이용하기 어려워짐
-   모든 서버가 모든 클라이언트의 상태 정보를 공유하는 작업은 복잡함
-   상태를 유지하지 않는 스테이트리스한 특성은 필요하다면 언제든 쉽게 서버를 추가할 수 있기 때문에 확장성이 높고, 서버 중 하나에 문제가 생겨도 쉽게 다른 서버로 대체가 가능하기 때문에 견고성이 높음
-   상태를 유지하지 않는 HTTP의 특성을 보완하기 위한 여러 방법이 있음

지속 연결 프로토콜

-   버전: HTTP1.1과 HTTP2.0이 포함
-   HTTP는 TCP상에서 동작하는데 HTTP는 비연결형 프로토콜이지만, TCP는 연결형 프로토콜임
-   HTTP버전 (HTTP 1.0이하)은 쓰리 웨이 핸드셰이크를 통해 TCP연결을 수립한 후, 요청에 대한 응답을 받으면 연결을 종료하는 방식으로 동작, 추가적인 요총- 응답을 하기 위해서는 다시 TCP연결을 수립하며 이런 방식을 비지속 연결이라고 함
-   최근 대중적으로 사용되는 HTTP버전(HTTP1.1이상)지속 연결이라는 기술을 제공 (킵 얼라이브)
-   하나의 TCP연결상에서 여러 개의 요청-응답을 주고받을 수 있는 기술
-   HTTP는 매번 새롭게 연결을 수립하고 종료해야 하는 비지속 연결에 비해 더 빠르게 여러 HTTP요청과 응답을 처리할 수 있음

## HTTP 메시지 구조

시작 라인
HTTP 요청 - 요청 라인
HTTP 응답 - 상태라인
헤더 라인
HTTP헤더
메서드(공백)요청 대상(공백) HTTP버전(줄바꿈)
HTTP버전(공백) 상태 코드(공백) 이유 구문 \* (줄바꿈)
줄바꿈
메시지 본문

### 시작 라인

HTTP 요청 - 요청 라인
HTTP응답 - 상태 라인
HTTP 요청 - 요청 라인 (메서드, 요청 대상, 버전)

-   메서드
    GET, POST, PUT, DELETE

### 요청 대상

HTTP요청을 보낼 서버의 자원
쿼리가 포함된 URI의 경로가 명시됨
하위 경로가 없더라도 요청 대상은 슬래시 / 로 표기해야 함

-   HTTP버전
    HTTP/1.1

### HTTP 응답 - 상태라인

상태 코드: 요청에 대한 결과를 나타내는 세자리 정수
이유 구문: 상태 코드에 대한 문자열 형태의 설명을 의미

## HTTP 메서드

GET : 자원을 습득하기 위한 메서드
HEAD : 서버로 하여금 특정 직업을 처리하게끔 하는 메서드
POST : 서버로 하여금 특정 직업을 처리하게끔 하는 메서드
PUT : 자원을 대체하기 위한 메서드
PATCH : 자원에 대한 부분적 수정을 위한 메서드
DELETE : 자원을 삭제하기 위한 메서드
CONNECT : 자원에 대한 양방향 연결을 시작하는 메서드
OPTIONS : 사용 가능한 메서드 등 통신 옵션을 확인하는 메서드
TRACE : 자원에 대한 루프백 테스트를 수행하는 메서드

## [좀 더 알아보기] HTTP의 발전: HTTP/0.9에서 HTTP/3.0

**HTTP/0.9**
지금은 거의 사용되지 않는 초창기 HTTP버전
사용 가능한 메서드가 GET뿐 요청 메시지는 한 줄로 구성되어 있었음
기능과 성능면에서 아주 제한적

**HTTP/1.0**
HEAD, POST 와 같은 GET 이외의 메서드가 도입
헤더가 지원되기 시작해 훨씬 더 다양한 정보를 주고받을 수 있게 됨
공식적으로는 지속 연결을 지원하지 않음
HTTP메시지를 주고받을 때마다 연결을 수립하고 종료하기를 반복함

**HTTP/1.1**
지속 연결이 공식적으로 지원되었음
특정 요청에 대한 응답이 수신되기 전에 다음 요청을 보낼 수 있는 파이프라이닝
다양한 편의 기능 및 사용 가능한 헤더가 추가되었음
오늘날까지 널리 사용되는 버전

**HTTP/2.0**
효울과 성능을 높이기 위한 버전
HTTP/1.1을 보완하고 개선하기 위한 버전으로 볼 수 있음
송수신 효율을 높이기 위해 헤더를 압축하여 전송
바이너리 데이터 기반의 메시지를 송수신함
클라이언트 요청하지 않더라도 미래에 필요할 것으로 예상되는 자원을 미리 전송해주는 서버 푸시라는 기능을 제공하기도 함
HOL블로킹 문제 완화한 버전 (같은 큐에 대기하며 순차적으로 처리되는 여러 패킷이 있을 때, 첫 번쨰 패킷의 처리 지연으로 인해 나머지 패킷들의 처리도 모두 지연되는 문제 상황을 의미)

**HTTP/3.0**
이전의 버전 모두 TCP를 기반으로 동작했지만 3.0 부터는 UDP를 기반으로 동작함
UDP를 기반으로 구현된 QUIC프로토콜을 기반으로 동작
연결형 프로토콜인 TCP에 비해 비연결형 프로토콜 UDP는 상대적으로 더 빠르기 때문에 속도 측면에 개선이 이루어짐
현재 빠르게 성장하는 프로토콜
QUIC의 중요성도 점차 커지고 있음
