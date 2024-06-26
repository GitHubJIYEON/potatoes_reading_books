## 📌 **학습 목표**

**허브, 반이중, 전이중, 콜라전 도메인, CSMA/CD**

통신 매체를 통해 송수신되는 메시지는 다른 호스트에게 전달되는 과정에서 네트워크 장비를 거칠 수 있고 네트워크 장비로

-   물리적인 계층에는 **허브,**
    -   허브의 동작 방식인 **반아중** 모드 통신 ↔ **전이중** 모드
    -   허브에서 발생하는 충돌이라는 문제와 이를 해결하기 위한 프로토콜인 CSMA/CD 도 학습
-   데이터 링크 계층에는 **스위치**

## 주소 개념이 없는 물리 계층

**물리 계층**

-   주소 개념 없음
-   호스트와 통신 매체 간의 연결과 통신 매체상의 송수신이 이루어짐
-   송수신되는 정보에 어떠한 조작(송수신 내용 변경)이나 판단을 하지 않음

**데이터 링크 계층**

-   주소 개념이 있음
-   MAC 주소가 속함
-   데이터 링크 계층의 장비나 그 이상 계층의 장비들은 송수신지를 특정할 수 있음
-   주소를 바탕으로 송수신되는 정보에 대한 조작과 판단을 할 수 있음

## 허브

**허브 (리피터 허브)** : 여러 대의 호스트를 연결하는 장치

**이더넷 허브**: 이더넷 네트워크의 허브

**허브의 특징**

-   오늘날 인터넷 환경에서 잘 사용되지 않음
-   전달받은 신호를 다른 모든 포트로 그대로 다시 내보냄
    -   신호를 전달 받으면 어떠한 조작이나 판단을 하지 않고 송신지를 제외한 모든 포트에 그저 내보내기만 함
    -   허브를 통해 이 신호를 전달받은 모든 호스트는 데이터 링크 계층에서 패킷의 max주소를 확인하고 자신과 관련 없는 주소는 폐기함
-   반아중 모드로 통신함
    -   반아중 모드 : 마치 1차선 도로처럼 송수신을 번갈아 가면서 하는 통신 방식
    -   ↔ 전이중 모드 : 마치 2차선 도로처럼 송수신을 동시에 양방향으로 할 수 있는 통신 방식
-   콜리전 도메인
    -   만일 동시에 허브에 신호를 송신하면 충돌 (콜리전)이 발생함
    -   충돌이 발생할 수 있는 영역을 **콜리전 도메인** 이라고 함
    -   콜리전 도메인은 작을수록 충돌이 발생할 가능성이 줄어듬
    -   허브의 넓은 콜라전 도메인으로 인한 충돌 문제를 해결하려면 CSMA/CD 프로토콜을 사용하거나 스위치 장비를 사용해야 함

## 허브 이외에 물리 계층의 대표적인 장비 **리피터**

-   전기 신호가 감소하거나 왜곡되는 것을 방지하기 위해 전기 신호를 증폭시켜 주는 장비
-   물리 계층의 장비
-   허브는 이러한 리피터의 기능을 포함하는 경우가 많음

## CSMA/CD

-   (Carrier Sense Multiple Access with Collision Detection) 의 약자
-   충돌 문제를 해결하기 위한 프로토콜
-   반아중 이더넷 네트워크에서 충돌을 방지하는 대표적인 프로토콜
-   이더넷을 대표하는 송수신 방법

**특징**

1. **CS는 Carrier Sense, 캐리어 감지를 의미**

-   현재 통신 매체의 사용 가능 여부를 검사하는 것
-   반송파 감지를 의미, 통신 매체상에서 흐르는 신호 감지

2. **MA는 Multiple Access, 다중 접근을 의미함**

-   두 개 이상의 호스트가 부득이하게 동시에 네트워크를 사용하려 할 때, 복수의 호스트가 네트워크에 접근하려는 상황을 **다중 접근**이라고 하며 이때 충돌이 발생함

3. **CD는 Collision Detection, 충돌 검출을 의미함**

-   충돌이 발생하면 이를 검출하는데 일를 **충돌 검출** 이라고함
-   충돌을 감지하면 전송이 중단, 충돌을 검출한 호스트는 다른 이들에게 충돌이 발생했음을 알리고 잼 신호라는 특별한 신호를 보냄 그리고 임의의 시간 동안 기다린 뒤에 다시 전송함

**정리**

CSMA/CD 프로토콜을 사용하면

1. 먼저 현재 전송이 가능한 상태인지 확인
2. 다른 호스트가 전송 중이지 않을 때 메시지를 전송
3. 만일 부득이하게 다수의 호스트가 접근하여 충돌이 발생하면 임의의 시간만큼 대기한 후 다시 전송
