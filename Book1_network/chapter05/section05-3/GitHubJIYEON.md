## HTTP 헤더

HTTP메시지

| 첫번째 라인 | 시작 라인, 메서드, 상태코드             |
| ----------- | --------------------------------------- |
| 두번째 라인 | HTTP헤더 - 필드 이름, 필드값, 콜론 기준 |

### 요청 시 활용되는 HTTP 헤더

1. **Host**

-   Host 는 요청을 보낼 호스트를 나타내는 헤더
-   주로 도메인 네임으로 명시 + 포트 번호 포함
    ```
    GET /hypertext/WWW/TheProject.html HTTP/1.1
    Host: info.cern.ch
    ```

2. **User-Agent**

-   User-Agent는 Host 헤더와 더불어 HTTP요청 메시지에서 가장 흔히 볼 수 잇는 헤더 중 하나
-   유저 에이전트란 웹 브라우저와 같이 HTTP요청을 시작하는 클라이언트 측의 프로그램을 의미
    [User-Agent] 요청 메시지 생성에 관여한 클라이언트 프로그램과 관련된 다양한 정보가 명시됨
    운영체제, 브라우저 종류 및 버전, 렌더링 엔진과 같은 다양한 정보가 Uwer-Agent헤더에 포함되어 있음을 알 수 있음
    서버 입자에서는 User-Agent 헤더를 통해 클라이언트의 접속 환경을 유추할 수 있음

3. **Referer**

-   클라이언트가 요청을 보낼 때 머무르고 있던 URL이 명시됨
    ```
    Referer: https://en.wikipedia.org/
    ```

4. **Authorization**

-   클라이언트의 인증 정보를 담는 헤더
-   가장 기본적인 HTTP 인증 타입은 Basic 이라는 타이
    username: password와 같이 사용자 아이디와 비밀번호를 콜론을 이용해 합친뒤, 이를 Base64 인코딩(문자를 코드로 변환하는 방법) 한 값을 인증 정보로 삼는 방식
        ```
        Authorization: <type> <credentials>

        Authorization: Basic bWluY2h1bDoxMjM0
        ```

### 응답 시 활용되는 HTTP 헤더

응답 시 주로 활용되는 대표적인 헤더

1.  Server
    Server 헤더는 요청을 처리하는 서버 측의 소프트웨어와 관련된 정보를 명시
    Unix운영체제에서 동작하는 아파치 HTTP서버 를 의미함
        ```
        Server: Apache/2.4.1 (Unix)
        ```
2.  Allow
    클라이언트에게 허용된 HTTP메서드 목록을 알려 주기 위해 사용
    요청한 메서드를 지원하지 않음 405상태코드 - Allow헤더와 함께 사용
3.  Retry-After
    503상태코드
    자원을 사용할 수 있는 날짜 혹은 시각을 나타냄
        ```
        Retry-after: Fri, 23 Aug 2024 90:00:00 GMT
        Retry-After: 120
        ```
4.  Location
    클라이언트에게 자원의 위치를 알려 주기 위해 사용되는 헤더
    리다이이렉션이 발생했을 때나 새로운 자원이 생성되었을 때 사용됨
5.  www-Authenticate
    상태코드 401
        ```
        WWW-Authenticate: Basic
        ```

**! 영역(realm)이란?**

1. 인증되지 않은 클라이언트가 서버에 GET요청 메시지를 전송합니다.
2. 서버는 클라이언트에게 상태코드 401과 함께 WWW-Atuhenticate헤더를 통해 인증 방식을 알립니다.
3. 클라이언트는 사용자로부터 인증 정보(사용자 아이디와 비밀번호)를 전달받습니다.
4. 사용자 아이디: 비밀번호 를 Base64 인코딩한 값을 인증 정보를 삼은 Atuhorization헤더를 통해 다시 GET 요청 메시지를 정송합니다.
5. 서버는 인증 정보를 확인합니다.
6. 인증이 유효하면 상태 코드 200으로 응답하고, 인증되지 않았으면 상태 코드 401로 응답함

### 요청과 응답 모두에서 활용하는 HTTP헤더

1.  Date
    생성된 날짜와 시각에 관련된 정보를 담은 헤더
        ```
        Date: Tue, 15 Nov 1994 08:12:31 GMT
        ```
2.  Connection
    클라이언트의 요청과 응답 간의 연결 방식을 설정하는 헤더
    Connection: keep-alive 헤더를 통해 상대방에게 지속 연결을 희망함을 알릴 수 있음
    서버나 클라이언트가 연결을 종료하고 싶을 때는 Connection-close를 통해 알릴 수 있음
    필드에는 다양한 값이 명시될 수 있지만, 가장 대표적으로 사용되는 값은 keep-alive 와 close입니다.
        ```
        Connection: keep-alive
        Connection: close
        ```
3.  Conent-length
    본문의 바이트 단위 크기(길이)를 나타냄
        ```
        Contnet-Length: 100
        ```
4.  Content-Type, Content-Language, Content-Encoding
    메시지 본문의 표현 방식을 설명하는 헤더
    표현헤더의 일종
    HTML문서 형식, 문자 인코딩으로 UTF-8을 사용한다는 정보를 알려줌
        ```
        Contnet-Length: text/html; charset=UTF-8
        ```

        - Content-Type
         메시지 본문에서 사용된 미디어 타입을 담고 있음
        - Content-Language
        헤더는 메시지 본문에 사용된 자연어를 명시
        어떤 언어로 작성되었는지 이를 통해 알 수 있음
        Ex) Content-en, Content-ko


            | 언어 | 언어 코드 |
            | --- | --- |
            | 한국어 | ko |
            | 영어 | en |
            | 중국어 | zh |
            | 일본어 | ja |
            | 독일어 | de |
            | 프랑스어 | fr |
        - Content-Encoding
        헤더에는 메시지 본문을 압축하거나 변환한 방식이 명시
        HTTP를 통해 송수신되는 데이터는 전송 속도를 개선하기 위해 종종 압축이나 변환이 되고는 하는데, 이때 사용된 방식이 Content-Encoidng필드에 명시되는 셈
        수신 측이 이 헤더를 통해 압축 및 변환 방식을 인식하고 압축을 해제하거나 원문으로 재변환하여 본문 내용을 확인할 수 있게 됨
        Content-Encoding 헤더의 명시될 수 있는 대표적인 값 : ‘gzip’, ‘compress’, ‘deflate’, ‘br’등

            ```
            Content-Encoding: gzip
            Content-Encoding: compress
            Content-Encoding: deflate
            Content-Encoding:br

            // 여러 인코딩이 사용되었을 경우: 적용된 순서대로 명시
            Content-Encoding: deflate, gzip
            ```


### 캐시

-   원본 데이터의 사본(원본이 아닌)을 임시로 저장하는 기술
-   캐시된 데이터를 캐시
-   불필요한 대역폭 낭비와 응답 지연을 방지하기 위해 정보의 사본을 임시로 저장하는 기술
-   정보의 사본을 임시로 저장하는 것 자체를 ‘캐시한다’, ‘캐싱한다’라고도 표현
-   사본을 임시로 저장해 두면 동일한 요청에 대해 캐시된 데이터를 활용할 수 있기 때문에 불필요한 대역폭 낭비를 줄일 수 있고, 더 빠르게 데이터에 접근할 수 있음

개인 전용 캐시 : 캐시는 웹 브라우저에 저장되어 있음
공용 캐시 : 클라이언트와 서버 사이에 위치한 중간 서버에 저장되어 있기도 함

캐시 신선도 : 사본 데이터가 얼마나 최신 원본 데이터와 유사한지를 표현함

신선도를 유지하는 가장 기본적인 방법은 캐시된 데이터에 유효 기간을 설정하는 방법

-   캐시 데이터에 유효 기간을 설정하고 기간이 만료되면 원본 데이터를 다시 요청하는 방식으로 캐시 신선도를 유지할 수 있음
-   캐시할 데이터에 유효 기간을 부여하는 방법으로 응답 메시지의 Expirse헤더(날짜) 와 **Cache-Contral헤더**의 Max-Age 값(초)을 사용할 수 있음

날짜를 기반으로 재검사하는 방식

클라이언트 If-Modified-Since헤더를 통해 서버에게 특정 시점 이후로 원본 데이터에 변경이 있었는지 물어볼 수 있음

응답 메시지

```

```

요청 메시지

```

```

### 쿠키

-   HTTP는 기본적으로 상태를 유지하지 않는 스테이트리스 프로토콜
-   서버에서 생성되어 클라이언트 측에 저장되는 데이터
-   상태를 유지하지 않는 HTTP의 특성을 보완하기 위한 수단
-   서버가 클라이언트의 상태를 알 수 있게끔 하는 특별한 데이터
-   쿠키를 이루는 정보는 기본적으로 <이름, 값>쌍의 형태를 띠고 있고, 추가로 적용 범위와 만료 기간 등 다양한 속성을 가질 수 있음
-   서버는 쿠키를 생성하여 클라이언트에게 전송하고, 클라이언트는 전달받은 쿠키를 저장해 뒀다가 추후동일한 서버에 보내느 ㄴ요청 메시지에 쿠키를 포함하여 전송합니다.
-   서버는 쿠키 정보를 참고해 두 개의 요청이 같은 클라이언트에서 왔는지, 로그인 상태를 유지하고 있는지 등을 알 수 있음

**!세션인증**

쿠키를 통해 전달되는 대표적인 정보로 세션 아이디 (session id)가 있습니다.

1. 클라이언트는 서버에게 (아이디, 비밀번호와 같은) 인증 정보를 전송합니다.
2. 인증 정보가 올바르다면, 서버는 세션 아이디를 생서앻 클라이언트에게 전송합니다.
3. 서버는 생성한 세션 아이디를 데이터베이스 등에 저장합니다.
4. 클라이언트는 추후 요청을 보낼 때 쿠키 내에 세션 아이디를 포함하여 전송합니다.
5. 서버는 쿠키 속 세션 아이디와 저장된 세션 아이디를 비교하여 클라이언트를 식별합니다.
   쿠키를 통해 세션 아이디를 전송하면 요청을 보낼 때마다 번거로운 인증 과정을 거칠 필요 없어 효율적임

응답 메시지

-   요청 메시지의 Cookie헤더 값은 서버에 전달할 쿸키의 이름과 값을 나타내는 헤더
    여러 개의 쿠키 값을 서버에 전달해야 할 때는 ; 세미 콜론을 사용하여 여러 쿠키의 이름-값을 나타낼 수 있음

```
Set-Cookie: 이름=값
Set-Cookie: 이름=값; 속성1
Set-Cookie: 이름=값; 속성1, 속성2
```

요청 메시지

```
Cookie: 이름=값; 이름=값
```

응답 메시지

```
HTTP/1.1/ 200 OK
Content-Type: text/html
Set-Cookie: name-minchul
Set-Cookie:phone=100-100
Set-Cookie:message=Hello
...헤더 생략
...메시지 본문 생략
```

요청 메시지

```
GET /next-page HTTP/1.1
Host: example.com
Cooke: name=minchul; phone=100-100, message=Hello
...헤더 후략
```

쿠키는 브라우저에서 저장되고 관리됨

console.log - Application→ Cookies 확인하면 쿠키 관련 정보로 이름과 값 외에도 도메인과 경로 등이 있음
ex) www.naver.com에게 받은 쿠키를 전혀 다른 웹 사이트인 www.google.com에게 전송하면 안되듯으, 쿠키는 사용 가능한 도메인이 정해져 있고 이는 응답 속 메시지 속 Set-Cookie 헤더의 ‘domain’속성을 정해짐

응답 메시지

```
Set-Coocke: name=minchul domain=example.com
```

응답 메시지

```
Set-Coocke: name=minchul path=/lectures
```

응답 메시지

```
Set-Coocke: sessionId=abc123; Expires=Fri, 23 Aug 2024 09:00:00 GMT
Set-Coocke: sessionId=abc123; Max-Age=2592000
```

**쿠키의 한계: 보안**

쿠키 정보가 쉽게 노출되거나 조작될 수 있다

이를 보완하기 위한 속성으로 Secure와 HttpOnly프로토콜 속성이 있음

HttpOnly

-   HttpOnly는 HTTP송수신을 통해서는 쿠키를 이용하도록 제한하는 속성
-   자바스크립트에서 쿠키를 중간에 가로채거나 위변조할 수 있음

### 콘텐츠 협상과 표현

HTTP의 콘텐츠 협상

-   같은 URI에 대해 가장 적합한 ‘자원의 형태’를 제공하는 메커니짐을 의미
-   한국어로 요청하면 한국어로 된 형태로 제공
-   송수신 가능한 자원의 형태를 자원의 **표현** 이라고 함
-   콘텐츠 협상은 클라이언트에게 가장 적합한 자원의 표현을 제공하는 메커니즘을 의미

요청 메시지

```
GET /index.html HTTP/1.1
Host: example.com
Accept-Language: ko
Accept- text/html
```

요청 메시지

```
GET /index.html HTTP/1.1
Host: example.com
Accept-Language: ko-KR,ko;q=0,9,en-US;q=0.7
Accept- text/html,application/xml;q=0, text/plain;q=0.6,*/*;q=0.5
```
