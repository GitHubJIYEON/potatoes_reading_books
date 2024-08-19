# 07-2 안전성을 위한 기술

**암호화**
원문 데이터를 알아볼 수 없는 형태로 변경하는 것을 의미
**복호화**
암호화된 데이터를 원문 데이터로 되돌리는 과정을 말함

**암호화와 복호화는** 비단 안전한 데이터 송수신뿐만 아니라 인증서 기반의 검증도 가능하게 합니다.

### 암호와 인증서

대칭 키 암호화 방식과 공개 키 암호화 방식

키: 컴퓨터 보안에서 사용되는 키는 무작위해 보이는 문자열처럼 보이나 키와 원문 데이터에 수학적 연산 과정을 거치면 암호문이 생성됨

이 수학적 연산 과정을 ‘암호화 알고리즘’ 이라고 불림

암호문을 수신자 측에서 복호화하면 원문 메시지를 얻을 수 있습니다.

**대칭 키 암호화** 방식

메시지를 암호화할 때 사용하는 키와 복호화할 때 사용하는 키가 동일합니다.

상대방에게 안전하게 키를 전달하기 어렵다는 점

키가 유출되면 큰 문제가 발생

**비대칭 키 암호화** 방식 (공개 키 암호화)

암호화를 위한 키와 복호화를 위한 키가 다름

한 키로 암호화 했다면 다른 키로 복호화 할 수 있음

한 쌍의 키를 각각 공개 키와 개인 키 라고 부름

공개 키만으로는 개인 키를 유추할 수 없고 반대로 개인 키만으로 공개 키를 유추할 수도 없음

공개 키로 암호화하고 개인 키로 복화할 수 있다면, 공개 키는 이름처럼 누구에게나 공개해도 무방, 반면 개인 키만큼은 절대로 유출되지 않도록 보안을 유지해야 함

인증서와 디지털 서명

인증서: 무엇인가를 증명하기 위한 문서를 의미, 네트워크(인터넷)에서 사용되는 ‘인증서’라는 용어는 일반적으로 공개 키 인정서를 일컫음

공개 키 인증서:

웹 서버는 공개 키뿐만 아니라 누가 생성했는지, 조작 되지는 않았는지, 유효 기간은 언제까지인지 등의 내용을 포함한 인증서를 전송함

공개 키가 포함되어 있다는 점 기억!

인증 기관 : 제 3의 기관에서 발급함, 인증 기관은 인증서의 발급, 검증, 저장과 같은 역할을 수행할 수 있는 공이니 기관 CA (대표적으로 IndenTrust, DigiCert, GlobalSign등)

서명 값: 클라이언트는 이 서명 값을 바탕으로 인증서를 검증할 수 있음

1. 인증서 내용에 대한 해시 값을 2. CA의 개인 키로 암호화하는 방식으로 만들어짐

CA는 이렇게 얻어낸 정보를 서명 값으로 삼아 클라이언트에게 인증서와 함께 전송합니다.

디지털 서명: 개인 키로 암호화된 메시지를 공개 키로 복호화함으로써 신원을 증명하는 이러한 절차를 **디지털 서명**이라고 함

## HTTPS: SSL과 TLS

-   인증과 암호화를 수행하는 프로토콜
-   TLS는 SSL을 계승한 프로토콜
-   작동 과정은 사용되는 암호 알고리즘과 버전에 따라 세부적인 차이가 있을 수 있으나
-   SSL/TLS 를 사용하는 대표적인 프로토콜 HTTPS
-   서버는 ClientHello 메시지에 대한 응답으로 ServerHello 메시지를 전송
-   ClientHello 메시지가 암호화 이전에 맞춰 봐야 할 정보들을 제시하는 메시지
-   ServerHello 메시지는 제시된 정보들을 선택하는 메시지
-   ClientHello와 ServerHello 메시지를 주고받으면 암호화된 통신을 위해 사전 협의해야 할 정보들이 결정됨 TLS 핸드셰이크에서의 키 교환, 이 단계 이후부터 클라이언트와 서버는 키 암호화된 암호문을 주고받을 수 있게 됩니다.