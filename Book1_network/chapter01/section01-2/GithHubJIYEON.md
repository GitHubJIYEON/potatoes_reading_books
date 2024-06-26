## 📌 Chapter01-2 네트워크 거시적으로 살펴보기

#네트워크구조 #LAN #WAN #회선교환 #패킷교환 #주소

#네트워크 기본 구조
그래프: 노드와 노드를 연결하는 간선으로 이루어진 자료구조
노드: 정보를 주고 받을 수 있는 장치
간선(링크): 노드를 연결하는, 유무선의 통신 매체 (유선, 무선)
메시지: 통신매체로 연결된 노드가 주고 받는 정보 (파일, 메일 등)

호스트(종단 시스템): 가장자리 노드
중간 노드: 네트워크 장비 (이더넷 허브, 스위치, 라우터, 공유기 등)가 될 수 있음

서버: '어떠한 서비스'를 제공하는 호스트
클라이언트: 서버에게 어떠한 서비스를 요청하고 서버의 응답을 제공받는 호스트

네트워크 장비: 호스트 간 주고 받을 정보가 중간에 거치는 중간 노드 (이더넷 허브, 스위치, 라우터, 공유기 등)

#범위에 따른 네트워크 분류
LAN (Local Area network) - 근거리 - 일반 가정, 특정 회사, 다른 국가의 가정, 학교

WAN (Wide Area Network) - 먼 지역을 연결하는 연결하는 광역 통신망을 의미 - ISP 인터넷 서비스 업체가 관리 구축함 - KT, LG유플러스, SK브로드밴드

더욱 세밀하게 하면? WAN > MAN > CAN > LAN

#메시지 교환 방식에 따른 네트워크 분류
회선 교환 방식

-   회선 : 먼저 메시지 전성로 설정
-   회선 스위치 : 회선 교환 네트워크 장비, 호스트 사이에 일대일 전송로를 확보하는 네트워크 장비
    장점: 두 호스트 사이에 연결을 확보한 후에 메시지를 주고받는 특성 덕분에 주어진 시간 동안 전송되는 정보의 양이 비교적 일정하다
    문제점: 회선의 효율이 낮아짐, 메시지가 흐르고 있어야 이용 효율이 높아지고 반대로 주고받지 않으면 회선 점유 낭비함

패킷 교환 방식

-   패킷 교환: 메시지를 패킷이라는 작은 단위로 쪼개어 전송
-   패킷: 패킷 교환 네트워크상에서 송수신되는 메시지의 단위
-   패킷 스위치 (라우터, 스위치): 패킷이 수신지까지 올바르게 도달할 수 있또록 최적의 경로를 결정하거나 패킷의 송수신
-   페이로드, 헤더, 트레일러, 주소
