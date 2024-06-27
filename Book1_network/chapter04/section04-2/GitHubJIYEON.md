전송 계층에서 가장 중요한 프로토콜은 TCP 와 UDP

TCP: 신뢰할 수 있는 통신을 위한 연결형 프로토콜

UDP: TCP보다 신뢰성은 떨어지지만 비교적 빠른 통신이 가능한 비연결형 프로토콜

## TCP 통신 단계와 세그먼트 구조

**TCP 통신의 3단계**

1. 연결 수립
2. 데이터 송수신
   재전송을 통한 오류 제어, 흐름 제어, 혼잡 제어
3. 연결종료

-   MMS라는 단위(TCP로 전송할 수 있는 최대 페이로드 크기, TCP 헤더 크기는 제외)
-   TCP의 세그먼트 구조

**TCP의 세그먼트 구조**

| 송신지 포트 | 공통     | 수신지 포트 |
| ----------- | -------- | ----------- |
|             | 순서번호 |             |

| 데이터 오프셋
예약
제어비트 | 확인 응답 번호 | 윈도우 |
| 체크섬 | | 긴급 포인터 |
| | 옵션 | |

-   **송신지 포트 와 수신지 포트**: 필드 이름 그대로 송신지 또는 수신지 애플리케이션을 식별하는 포트 번호가 명시되는 필드
-   **순서 번호**: 순서 번호가 명시되는 필드, 순서 번호란 송수신되는 세그먼트의 올바른 순서를 보장하기 위해 세그먼트 데이터의 첫 바이트에 부여되는 번호
-   **확인 응답 번호** : 상대 호스트가 보낸 세그먼트에 대한 응답, 다음으로 수신하기를 기대하는 순서 번호가 명시됨
    -   순서 번호와 확인 응답번호: TCP의 신뢰성을 보장하기 위해 사용되는 중요한 필드,
        이 두 필드에는 각각 순서 번호와 확인 응답 번호가 명시됨
        한 쌍으로 묶어서 기억하는 것이 좋음
    -   순서 번호: 세그먼트의 올바른 송수신 순서를 보장하기 위한 번호, 세그먼트 데이터의 첫 바이트에 부여되는 번호로 MMS 단위로 전송 됨
    -   제어 비트에서 연결을 수립하기 위한 비트인 SYN 플래그가 1로 설정된 세그먼트의 경우 순서 번호는 무작위 값이 되며 이를 초기 순서 번호 라고 함
    -   연결 수립 이후 데이터를 송수신하는 동안 순서 번호는 송신한 바이트를 더해 가는 형태로 누적값을 가짐
    -   즉, 순서 번호는 초기 순서 번호(초기 순서 번호) + 송신한 바이트 수 (떨어진 바이트 수)
    -   확인 응답 번호 필드: 확인 응답 번호는 순서 번호에 대한 응답
-   **제어 비트 (플래그 비트)**: 현재 세그먼트에 대한 부가 정보를 나타냄
    -   기본적으로 8비트로 구성
    -   ACK: 세그먼트의 승인을 나타내기 위한 비트
    -   SYN: 연결을 수립하기 위한 비트
    -   FIN: 연결을 종료하기 위한 비트
-   **윈도우**: 수신 윈도우의 크기가 명시됨 (수신 윈도우: 한 번에 수신하고자 하는 데이터의 양)

## TCP 연결 수립과 종료

**연결 수립**

-   쓰리 웨이 핸드셰이크: 세 개의 단계로 이루어진 TCP의 연결 수립 과정을 의미

| 송수신 방향           | 세그먼트           | 세그먼트에 포함된 주요 정보 | 비유 |
| --------------------- | ------------------ | --------------------------- | ---- |
| A → B                 | SYN 세그먼트       | - 호스트 A의 초기 순서 번호 |
| - 1로 설정된 SYN 비트 | ‘연결 시작합니다.’ |
| B → A                 | SYN + ACK 세그먼트 | - 호스트 B의 초기 순서 번호 |

-   호스트 A가 전송한 세그먼트에 대한 확인 응답 번호
-   1로 설정된 SYN비트
-   1로 설정된 ACK 비트 | ‘네, 확인했습니다.
    연결 시작해요!’ |
    | A → B | ACK 세그먼트 | - 호스트 A의 다음 순서 번호
-   호스트 B가 전송한 세그먼트에 대한 확인 응답 번호
-   1로 설정된 ACK비트 | ‘네, 확인했습니다.’ |
-   처음 연결을 시작하는 호스트의 연결 수립 과정을 액티브 오픈
    -   서버 - 클라이언트 관계에서 클라이언트에 의해 수행
    -   A의 동작
-   반대로 연결 요청을 받고 나서 요청에 따라 연결을 수립해주는 호스트의 수립 과정을 패시브 오픈
    -   주로 서버에 의해 수행됨
    -   B의 동작

**연결 종료**

-   TCP가 연결을 종료하는 과정은 송수신 호스트가 각자 한 번씩 FIN과 ACK를 주고받으며 이루어짐

| 송수신 방향           | 세그먼트           | 세그컨트에 포함된 주요 정보                          | 비유               |
| --------------------- | ------------------ | ---------------------------------------------------- | ------------------ |
| A → B                 | FIN 세그먼트       | - 1로 설정된 FIN                                     | ‘연결 끊을게요’    |
| B → A                 | ACK 세그먼트       | - 호스트 A가 전송한 세그먼트에 대한 확인 응답 번호   |
| - 1로 설정된 ACK 비트 | '네 확인했습니다’  |
| B → A                 | FIN 세그먼트       | - 1로 설정된 FIN비트                                 | ‘이제 연결 끊어요’ |
| A → B                 | ACK 세그먼트       | - 호스트가 B가 전송한 세그먼트에 대한 확인 응답 번호 |
| - 1로 설정된 ACK비트  | '네, 확인했습니다’ |

액티브 클로즈 : 먼저 연결을 종료하려는 호스트에 의해 수행, 호스트 A가 액티브 클로즈 수행

패시브 클로즈: 연결 종료 요청을 받아들이는 호스트, 호스트 B의 동작

## TCP 상태

**TCP**

-   연결형 통신과 신뢰할 수 있는 통신을 유지하기 위해 다양한 ‘상태 (현재 어떤 통신 과정에 있는지를 나타내는 정보)’를 유지합니다.
-   TCP는 상태를 유지하고 활용한다는 점에서 스테이트풀 프로토콜이라고도 함

**연결이 수립되지 않은 상태**

-   CLOSED(아무런 연결이 없는 상태) LISTEN(일종의 연결 대기 상태) 상태를 유지
-   LISTEN상태는 쓰리 웨이 핸드셰이크의 첫 단계의 액티브 오픈 호스트가 LISTEN상태인 호스트 (일반적 서버) 에게 SYN세그먼트를 보내면 쓰리 웨이 핸드셰이크가 시작됨

**연결 수립 상태**

-   TCP 연결 수립 과정, SYN-SENT, SYN-RECEIVED, ESTABLISHED 상태
-   SYN-SENT: 액티브 호스트가 SYN 세그먼트를 보낸 뒤 그에 대한 응답인 SYN+ACK세그먼트를 기다리는 상태, 연결 요청 보낸 뒤 대기하는 상태
-   SYN-RECEIVED: 패시브 오픈 호스트가 SYN+ACK세그먼트를 보낸 뒤 그에 대한 ACK세그먼트를 기다리는 상태
-   ESTABLISHED: 연결이 확립되었음을 나타내는 상태, 데이터를 송수신할 수 있는 상태를 의미
    쓰리 웨이 핸드셰이크 과정에서 두 호스트가 마지막 ACK세그먼트를 주고 받으면 ESTABLISHED상태로 접어들게 됨

**연결 종료 상태**

-   TCP 연결을 종료하는 과정, FIN-WAIT-1, CLOSE-WAIT, FIN-WAIT-2, LAST-ACK, TIME-WAIT, CLOSED상태
-   FIN-WAIT-1: 연결 종료의 첫 단계
-   CLOSE-WAIT: 종료 요청인 FIN세그먼트를 받은 패시브 클로즈 호스트가 그에 대한 응답으로 ACK세그먼트를 보낸 후 대기하는 상태
-   FIN-WAIT-2: 상대 호스트의 FIN세그먼트를 기다리는 상태
-   LAST-ACK: ACK세그먼트를 기다리는 상태
-   TIME-WAIT: 액티브 클로즈 호스트가 FIN세그먼트를 수신한 뒤, 이에 ACK세그먼트를 전송한 뒤 접어드는 상태
-   CLOSED: TIME-WAIT 상태에 접어든 택티브 클로즈 호스트는 일정 시간을 기다린 뒤 CLOSED상태로 전이함

## UDP 데이터그램 구조

**UDP**

-   비연결형 통신을 수행하는 신뢰할 수 없는 프로토콜
-   연결 수립 및 해제, 재전송을 통한 오류 제어, 혼잡 제어, 흐름 제어 등을 수행하지 않음
-   TCP처럼 상태를 유지하지도 않는 점에서 스테이트리스 프로토콜의 일종이라고 함
-   TCP 비해 제공하는 기능이 적어 필드도 단순함
-   송신지 포트, 수신지 포트, 길이, 체크섬 필드

| 송신지 포트 | 수신지 포트 |
| ----------- | ----------- |
| 길이        | 체크섬      |

-   송신지 포트와 수신지 포트: 송수신지의 포트 번호
-   길이: 헤더를 포함한 UDP 데이터그램의 바이트가 담김
-   체크섬: 데이터그램 전송 과정에서 오류가 발생했는지 검사하기 위한 필드
    ’수신지까지 잘 도달했는지’를 나타내는 신뢰성/비신뢰성과는 관련이 없음