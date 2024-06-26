**NIC**

-   호스트와 통신 매체를 연결
-   MAC주소가 부여되는 네트워크 장비

**케이블 :** NIC에 연결되는 물리 계층의 유선 통신 매체

-   트위스티드 페어 케이블
-   광섬유 케이블

---

## NIC

호스트와 유무선 통신 매체를 연결하고 이러한 변환을 담당하는 네트워크 장비가 NIC

### **NIC 생김새**

-   인터페이스 카드, 네트워크 어댑터, LAN카드, 네트워크 칻, 이더네 카드(이더넷 네트워크의 경우)등 다양한 명칭으로 불림
-   확장 카드 형태로 따로 연결하여 사용했기에 ‘카드’라고 함
-   확장 카드는 컴퓨터에 기능을 추가할 목적으로 연결하는 카드 형태의 회로 기판임

### **NIC의 역할**

-   NIC는 통신 매체에 흐르는 신호를 호스트가 이해하는 프레임으로 변환
    또는 호스트가 이해하는 프레임을 통신 매체에 흐르는 신호로 변환함
-   NIC는 네트워크와의 연결점을 담당하는 점에서 네트워크 인터페이스 역할을 수행한다고도 함

## 트위스티드 페어 케이블

**트위스티드 페어 케이블**

-   구리 선으로 전기 신호를 주고받는 통신 매체
-   LAN케이블이라고 하면 가장 먼저 떠오를 만큼 대중적인 케이블 중 하나

**케이블 본체** : 트위스티드 페어 케이블

**케이블의 연결부**: 커넥터

트위스티드 페어 케이블에서 주로 활용되는 커넥터를 RJ-45라고 부름

노이즈 : 구리 선으로 이루어진 상태에서 전기 신호를 주고받다 보면 구리 선에 전자적 간섭이 생길 수 있는 점 이렇게 신호를 왜곡시킬 수 있는 간섭을 노이즈 라고 부름

차폐: 구리선 주변을 감싸 노이즈를 감소시키는 방식

브레이드 실드 or 포일 실드차폐에 사용된 그물 모양의 철사와 포일을 각각

실드에 따른 트위스티드 페어 케이블의 분류

## 광섬유 케이블

**광섬유 케이블의 생김새**

-   케이블 본체와 커넥터로 이루어짐
-   LC커넥터, SC커넥터, FC커넥터, ST커넥터

**광섬유 한 가닥을 확대해서 관찰하면?**

-   코어 : 광섬유의 중심
-   클래딩 : 코어를 둘러싸고 빛이 코어 안에서만 흐르도록 빛을 가두는 역할을 함
-   코어의 지름에 따라 나누어지는 싱글 모드와 멀티 모드의 광섬유 테이블

**싱글 모드 광섬유 케이블**

-   코어의 지름 1mm 는 1,000um (머리카락 평균 두께 대략 50~150um)
-   굉장히 작음
-   싱글 모드 케이블은 신호 손실이 적기에 장거리 전송에 적합
-   멀티 모드에 비해 비용이 높은 단점 있음
-   파장이 긴 장파장의 빛을 사용함
-   대표적으로 싱글 모드 광섬유 케이블 규격으로 1000BASE-LX, 10GBASE-LR 있음
-   L은 장파장을 의미

**멀티 모드 광섬유 케이블**

-   코어의 지름 50~62.5um정도로 싱글 모드보다 큼
-   그림처럼 빛이 여러 경로로 이동할 수 있음 → 모드가 여러개라고 표현함
-   싱글모드보다 전송 시 신호 손실이 클 수 있기에 장거리에 전송에는 부적합
-   일반적으로 수백 미터, 길어야 수 킬로미터 정도만 전송이 가능
-   비교적 근거리를 연결하는데 주로 사용
-   싱글 모드에 비해 단파장의 빛을 사용
-   대표적인 멀티 모드 케이블 규격은 1000BASE-SX, 10GBASE-SR이 있음
-   여기서 S는 단파장을 의미

**케이블 색상으로 분류하는 싱글 모드와 멀티 모드**

싱글 모드: 광섬유 케이블의 본체는 대부분 노란색과 파란색

멀티 모드: 광섬유 케이블은 오렌지색과 아쿠아색
