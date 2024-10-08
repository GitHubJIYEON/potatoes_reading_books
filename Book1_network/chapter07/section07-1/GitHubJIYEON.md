# 07-1 안전성을 위한 기술

사용자가 폭증하면 불안정해지고 부하가 가중된다?

안전성을 높이는 방법

-   물리적 장비나 프로그램 등을 여러 개 두는 기술 - 이중화, 다중화
-   트래픽을 고르게 분산하는 기술 - 로드 밸런싱

**가용성**

안전성: 특정 기능을 언제든 균일한 성능으로 수행할 수 있는 특성

-   안정적인 웹 서버 → 언제든지 응답 메시지를 제공할 수 있는 서버 의미
-   안정적인 라우터 → 언제든지 라우팅 기능을 제공할 수 있는 라우터를 의미

가용성: 컴퓨터 시스템(서버, 네트워크, 프로그램 등)이 특정 기능을 실제로 수행할 수 있는 시간의 비율을 의미

전체 사용 기간 중에서 정상적인 사용 시간을 의미

정상적인 사용 시간 : 업타임

정상적인 사용이 불가능한 시간: 다운타임

가용성 = 업타임 / 업타임+다운타임

가용성을 높이려면?

-   다운타임을 낮추어야 함
-   과도한 트래픽에 인해 서비스가 다운될 수 있고, 소프트웨어상의 오류, 하드웨어 장애가 원인일 수도 있고, 보안 공격, 자연재해로 인해 서비스가 다운 될 수도 있다. 원인을 모두 찾아 원천적으로 차단하기는 현실적으로 어렵다.
-   결함 감내: 문제가 발생하더라도 기능할 수 있는 능력
-   다운타임을 낮추고 가용성을 높이기 위해서는 결함을 감내할 수 있도록 서비스나 인프라를 설계하는 것이 중요

**이중화**

이중화: 무언가를 이중으로 두는 기술

-   결함을 감내하여 가용성을 높이기 위한 가장 근본적이고 대표적인 방법
-   예비(백업)를 마련하는 방법

단일 장애점: 문제가 발생할 경우 시스템 전체가 중단될 수 있는 대상

-   SPOF 라우터: 라우터가 고장나면 서버로부터 제공받는 서비스 전체가 동작하지 않아 SPOF는 최대한 없애는 것이 좋고 가용성을 높이기 위해서는 SPOF를 이중화하는 것이 좋음

**이중화 구성**

액티브: 가동상태를 의미
스탠바이: 액티브의 백업으로서 대기하는 상태를 의미

-   액티브/스탠바이
    한 시스템은 가동하고 다른 시스템은 백업 용도로 대기 상태(스탠바이)로 두는 이중화 구성 방식
    액티브 상태인 시스템에 문제가 발생할 경우 스탠바이 시스템이 자동으로 액티브 시슽템을 대신하여 동작 - 안전한 구성방식이나 하나의 장비를 사용 할 때에 비해 성능상의 큰 변화르 기대하기는 어려움
-   액티브/액티브
    두 시스템 모두를 가동 상태로 두는 구성 방식을 의미
    부하를 분산시킬 수 있고 두 시스템이 함께 가동되므로 성능상의 이점도 있음
    다만 한 시스템에 문제가 발생하면 순간적으로 다른 시스템에 부하가 급증할 수 있으며 이로 인해 추가적인 문제가 발생할 수 있음
-   이중화 기술 : 무언가를 이중으로 두는 기술
-   다중화 기술: 무언가를 여러 개 두는 기술

이중화/다중화 사례

티밍: 윈도우 사용되는 용어, 액티브/액티브 구성 or 액티브/스탠바이로 구성할지 선택 가능

본딩: 리눅스 사용되는 용어,

여러 개의 네트워크 인터페이스를 이중화/다중화하며 마치 더 뛰어나고 안정적인 성능을 보유한 하나의 인터페이스처럼 보이게 하는 기술

**로드 밸런싱**

고가용성을 요구하는 호스트는 클라이언트보다는 일반적으로 서버

서버 입장에서 가용성 : 서버를 다중화했더라도 트래픽 분배 문제

트래픽 : 주어진 시점에 네트워크를 경유한 데이터의 양
일반적인 트래픽 측정은 노드에서 이루어지므로 일반적으로 표현하면 주어진 시점에 특정 노드를 경유한 패킷의 양

서버에 과도한 트래픽이 몰리면?

-   높은 부하로 CPU는 발열 심해짐
-   메모리 공간은 수많은 트래픽 내용을 저장하기에 부족
-   제한된 대역폭과 병목 현상으로 인해 응답이 느려지거나 일부 요청에 대한 응답이 누락될 수 있음
-   프로그램의 일관성이 손상될 수 있음
-   과도한 트래픽은 서버의 가용성을 떨어뜨림
-   다중화했더라도 트래픽을 고르게 분산해야 가용성이 높아짐

로드 밸런싱: 부하를 의미하는 단어의 로드와 균형을 유지하는 단어 밸런싱 합쳐진 단어

-   로드 밸런싱은 로드 밸런서에 의해 수행
-   로드 밸런서는 L4스위치, L7 스위치 라 불리는 네트워크 장비로도 수행할 수 있지만 로드 밸런싱 기능을 제공하는 소프트웨어를 설치하면 일반 호스트로 로드 밸런서로 사용할 수 있음
-   대표적 소프트웨어 HAProxy, Envoy등
-   웹 서버 소프트웨어 Nginx 에도 로드 밸런싱 기능이 내포
-   로드 밸런서: 이중화나 다중화된 서버와 클라이언트 사이에 위치

**로드 밸런싱 알고리즘**

-   라운드 로빈 알고리즘
-   최소 연결 알고리즘
-   해시라는 자료 구조를 이용하기도 함
-   응답 시간이 짧은 서버를 선택하기도 함
-   가중치 라운드 로빈 알고리즘
-   가중치 최소 연결 알고리즘

[ 좀 더 알아보기 ] 포워드 프록시와 리버스 프록시

실제로 클라이언트와 서버 사이에는 수많은 서버 존재

자원을 생성하고 클라이언트에게 권한 있는 응답을 보낼 수 있는 HTTP 서버 - 오리진서버

인바운드: 오리진 서버를 향하는 메시지를 의미

아웃바운드: 클라이언트를 향하는 메시지를 의미

HTTP의 중간 서버의 유형

-   프록시 (포워드 프록시) : 클라이언트가 선택한 메시지 전달 대리자, 클라이언트들을 대신해 대저택(오리진서버) 에 심부름을 가는 심부름꾼
-   게이트웨이 ( 리버스 프록시) : 연결에 대해 오리진 서버 역할을 하지만, 수신된 요청을 변환하여 다른 인바운드 서버들로 전달하는 중개자 역할, 오리진 서버들에 더 가까이 위치함,
    게이트웨이도 캐시를 저장할 수 있고, 로드 밸런서로 동작할 수 있음, 대저택(오리진서버)를 지키는 경비
