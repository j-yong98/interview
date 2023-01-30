TCP/IP 4계층 모델
=
- 인터넷 프로토콜 스위트는 인터넷에서 컴퓨터들이 서로 정보를 주고받는 데 쓰이는 프로토콜의 집합이며, 이를 TCP/IP 4계층 모델로 설명하거나 OSI 7계층 모델로 설명하기도 합니다.
- TCP/IP 모델은 네트워크에서 사용되는 통신 프로토콜의 집합으로 계층들은 프로토콜의 네트워킹 범위에 따라 네 개의 추상화 계층으로 구성됩니다.
***
### 계층 구조
    TCP/IP구조에서는 네 개의 계층을 가지고 있으며 OSI 7계층과 많이 비교합니다.
    - TCP/IP 계층
        - 애플리케이션 계층
        - 전송 계층
        - 인터넷 계층
        - 링크 계층
    - OSI 7계층
        - 애플리케이션 계층
        - 프레젠테이션 계층
        - 세션 계층
        - 전송 계층
        - 네트워크 계층
        - 데이터 링크 계층
        - 물리 계층
 - TCP/IP 계층과 달리 OSI 계층은 애플리케이션 계층을 세 개로 쪼개고 링크 계층을 데이터 링크 계층, 물리 계층으로 나누어 표현 하는 것이 다르다.
 - 인터넷 계층을 네트워크 계층으로 부른다는 점도 다르다.
 - 이 계층들은 특정 계층이 변경 되더라도 다른 계층이 영향 받지 않는 구조로 설계 되어 있습니다.
***
 - 애플리케이션 계층
   - 애플리케이션 계층은 FTP, HTTP, SSH, SMTP, DNS 등 응용 프로그램이 사용되는 프로토콜 계층이며 웹 서비스, 이메일 등 서비스를 실질적으로 사람들에게 제공 하는 층입니다.
   - <strong>FTP</strong>
     - 장치와 장치간의 파일을 전송하는 데 사용하는 표준 통신 프로토콜
   - <strong>SSH</strong>
     - 보안 되지 않은 네트워크에서 네트워크 서비스를 안전하게 운영하기 위한 암호화 네트워크 프로토콜
   - <strong>HTTP</strong>
     - World Wide Web을 위한 데이터 통신의 기초이자 웹 사이트를 이용하는데 쓰는 프로토콜
   - <strong>SMTP</strong>
     - 전자 메일 전송을 위한 인터넷 표준 통신 프로토콜
   - <strong>DNS</strong>
     - 도메인 이름과 IP 주소를 매핑해주는 서버
***
 - 전송 계층
   - 전송 계층은 송신자와 수신자를 연결하는 통신 서비스를 제공하며 연결 지향 데이터 스트림 지원, 신뢰성, 흐름 제어를 제공할 수 있으며 애플리케이션과 인터넷 계층 사이의 데이터가 전달될 때 중계 역할을 합니다.
   - <strong>TCP</strong>
     - TCP는 패킷 사이의 순서를 보장하고 연결지향 프로토콜을 사용해서 연결을 하여 신뢰성을 구축해서 수신 여부를 확인하며 '<strong>가상회선 패킷 교환 방식</strong>'을 사용합니다.
     - <strong>가상회선 패킷 교환 방식</strong>
       - 가상회선 패킷 교환 방식은 각 패킷에는 가상회선 식별자가 포함되어 모든 패킷을 전송하면 가상회선이 해제되고 패킷들은 전송된 '순서대로' 도착하는 방식을 말합니다.
     - TCP 연결 성립 과정
       - TCP는 신뢰성을 확보할 때 '3-way handshake'라는 작업을 진행하게 됩니다.
         1. SYN 단계 : 클라이언트는 서버에게 클라이언트의 ISN을 담아 SYN을 보냅니다. ISN은 새로운 TCP연결의 첫 패킷에 할당된 임의의 시퀀스 번호를 말하며 이는 장치마다 다를 수 있습니다.
         2. SYN + ACK 단계 : 서번튼 클라이언트의 SYN을 수신하고 서버의 ISN을 ㅂ보내며 승인번호로 클라이언트의 ISN + 1을 보냅니다.
         3. ACK 단계 : 클라이언트는 서버의 ISN + 1한 값인 승인번호를 담아 ACK를 서버에 보냅니다.
     - 이렇게 3-way handshake 과정 이후 신뢰성이 구축되고 데이터 전송을 시작합니다. 이 과정이 있기 때문에 TCP는 신뢰성이 있는 계층이라합니다.
     - TCP 연결 해제 과정
       - TCP는 연결을 해제할 때는 4-way handshake 과정이 발생합니다.
         1. 클라이언트가 연결을 닫으려고 할 떄 FIN으로 설정된 세그먼트를 보냅니다. 그리고 클라이언트는 FIN_WAIT_1 상태로 들어가고 서버의 응답을 기다립니다.
         2. 서버는 클라이언트로 ACK라는 승인 세그먼트를 보냅니다. 그리고 CLOSE_WAIT 상태에 들어갑니다. 클라이언트가 세그먼트를 받으면 FIN_WAIT2 상태에 들어갑니다.
         3. 서버는 ACK를 보내고 일정 시간 이후에 클라이언트에 FIN이라는 세그먼트를 보냅니다.
         4. 클라이언트는 TIME_WAIT 상태가 되고 다시 서버로 ACK를 보내서 서버는 CLOSED 상태가 됩니다. 이후 클라이언트는 어느 정도의 시간을 대기한 후 연결이 닫히고 클라이언트와 서버의 모든 자원의 연결이 해제 됩니다.
        - 이 과정에서 중요한 것은 TIME_WAIT입니다. 그냥 연결을 닫으면 되지 왜 굳이 일정 시간 뒤에 닫을 까요??
          - 첫 번째는 지연 패킷이 발생할 경우를 대비하기 위함입니다. 패킷이 뒤늦게 도달하고 이를 처리하지 못한다면 데이터 무결성 문제가 발생합니다.
          - 두 번쨰는 두 장치가 연결이 닫혔는지 확인하기 위해서입니다. LAST_ACK 상태에서 닫히게 되ㅣ면 다시 새로운 연결을 하려고 할 때 장치는 줄곧 LAST_ACK로 되어 있기 때문에 접속 오류가 나타나게 될 것입니다.
   - <strong>UDP</strong>
     - UDP는 순서를 보장하지 않고 수신 여부를 확인하지 않으며 단순히 데이터만 주는 '<strong>데이터그램 패킷 교환 방식</strong>'을 사용합니다.
     - <strong>데이터그램 패킷 교환 방식</strong>
       - 데이터그램 패킷 교환 방식이란 패킷이 독립적으로 이동하며 최적의 경로를 선택하여 가는데, 하나의 메시지에서 분할된 여러 패킷은 서로 다른 경로로 전송될 수 있으며 도착한 '순서가 다를 수' 있는 방식을 뜻합니다.
###### 데이터 무결성 - 데이터의 정확성과 일관성을 유지하고 보증하는 것

***
 - 인터넷 계층
   - 장치로부터 받은 네트워크 패킷을 IP 주소로 지정된 목적지로 전송하기 위해 사용되는 계층입니다.
   - IP, ARP, ICMP 등이 있으며 패킷을 수신해야 할 상대의 주소를 지정하여 데이터를 전달합니다.
   - 상대방이 제대로 받았는지에 대해 보장하지 않는 비연결형적인 특징을 가지고 있습니다.
***
 - 링크 계층
   - 전선, 광섬유, 무선 등으로 실질적으로 데이터를 전달하며 장치 간에 신호를 주고 받는 '규칙'을 정하는 계층입니다. 
   - 네트워크 접근 계층이라고도 합니다.
   - 이를 물리 계층과 데이터 링크 계층으로 나누기도 하는데 한다.
   - 물리 계층은 무선 LAN과 유선 LAN을 통해 0과 1로 이루어진 데이터를 보내는 계층을 말한다.
   - 데이터 링크 계층은 '이더넷 프레임'을 통해 에러 확인, 흐름 제어, 접근 제어를 담당하는 계층을 말한다.
   - 유선 LAN(IEEE802.3)
     - 유선 LAN을 이루는 이더넷은 IEEE802.3이라는 프로토콜을 따르며 전이중화 통신을 씁니다.
     - <strong>전이중화 통신</strong>
       - 전이중화 통신은 양쪽 장치가 동시에 송수신할 수 있는 방식을 말합니다.
       - 송신로와 수신로로 나눠서 데이터를 주고받으며 현대의 고속 이더넷은 이 방식을 기반으로 통신하고 있습니다.
     - CSMA/CD
       - 이전 유선 LAN에 '반이중화 통신' 중 하나인 CSMA/CD (Carrier Sense Multiple Access with Collision Detection) 방식을 썼습니다.
       - 이 방식은 데이터를 보낸 이후 충돌이 발생한다면 일정시간 이후 재전송하는 방식을 말합니다.
       - 이는 수신로와 송신로를 각각 둔 것이 아니고 한 경로를 기반으로 데이터를 보내기 때문에 데이터를 보낼 때 충돌에 대비를 해야 했기 때문입니다.
     - 유선 LAN을 이루는 케이블
       - 유선 LAN을 이루는 케이블로는 TP 케이블이라고 하는 트위스트 페어 케이블과 광섬유 케이블이 대표적입니다.
       - 트위스트 페어 케이블
         - 트위스트 페어 케이블(Twisted pair cable)은 하나의 케이블처럼 보이지만 실제로는 여덟개의 구리선을 두 개씩 꼬아서 만든 케이블입니다.
         - 케이블은 구리선을 실드 처리하지 않고 덮은 UTP케이블과 실드 처리하고 덮은 STP로 나눠집니다.
         - 흔히 UTP 케이블을 랜선이라고합니다.
       - 광섬유 케이블
         - 광섬유로 만든 케이블입니다.
         - 레이저를 이용해서 통신하기 때문에 구리선과는 비교할 수 없을 만큼 장거리 및 고속 통신이 가능합니다. 보통 100Gps의 데이터를 전송하며 다음 그림처럼 광섬유 내부와 외부를 다른 밀도를 가지는 유리나 플라스틱 섬유로 제작해서 한 번 들어간 빛이 내부에서 계속적으로 반사하며 전진하여 반대끝까지 가는 원리
         - 빛의 굴절률이 높은 부분을 코어라고 하며 낮은 부분을 클래딩이라고 합니다.
   - 무선 LAN(IEEE802.11)
     - 무선 LAN 장치는 수신과 송신에 같은 채널을 사용하기 때문에 반이중화 통신을 사용합니다.
     - 반이중화통신
       - 반이중화 통신(half duplex)은 양쪽 장치는 서로 통신할 수 있지만, 동시에는 통신할 수 없으며 한 번에 한 방향만 통신할 수 있는 방식을 말합니다.
       - 일반적으로 장치가 신호를 수신하기 시작하면 응답하기 전에 전송이 완송될 때까지 기다려야 합니다. 또한, 둘 이상의 장치가 동시에 전송하면 충돌이 발생하여 메시지가 손실 되거나 왜곡될 수 있기 때문에 충돌 방지 시스템이 필요합니다.
     - CSMA/CA
       - CSMA/CA는 반이중화 통신 중 하나로 장치에서 데이터를 보내기 전에 캐리어 감지 등으로 사전에 가능한 한 충돌을 방지하는 방식을 사용하며 과정은 다음과 같다.
         1. 데이터를 송신하기 전에 무선 매체를 살핍니다.
         2. 캐리어 감지 : 회선이 비어 있는지를 판단합니다.
         3. IFS(Inter FrameSpace) : 랜덤 값을 기반으로 정해진 시간만큼 기다리며,ㅡ 만약 무선 매체가 사용 중이면 점차 그 간격을 늘려가며 기다립니다.
         4. 이후에 데이터를 송신합니다.
       - 전이중화 통신은 양방향 통신이 가능하기 때문에 충돌 가능성이 없어 충돌을 감지하거나 방지하는 메커니즘이 필요하지 않습니다.
     - 무선 LAN을 이루는 주파수
       - 무선 LAN은 무선 신호 전달 방식을 이용하여 2대 이상의 장치를 연결하는 기술이다.
       - 비유도 매체인 공기에 주파수를 쏘아 무선 통신망을 구축하는데, 주파수 대역은 2.4GHz대역 또는 5GHz 대역 중 하나를 써서 구축합니다.
       - 2.4GHz는 장애물에 강한 특성을 가지고 있지만 전자레인지, 무선 등 전파 간섭이 일어나는 경우가 많다.
       - 5GHz 대역은 사용할 수 있는 채널 수도 많고 동시에 사용할 수 있기 때문에 상대적으로 깨끗한 전파 환경을 구축할 수 있습니다.
       - 그렇기 떄문에 보통은 5GHz 대역을 사용하는 것이 좋습니다.
       - 와이파이(wifi)
         - 전자기기들이 무선 LAN 신호에 연결할 수 있게 하는 기술로 이를 사용하려면 AP(Access Point)가 있어야 합니다.
         - 흔히 AP를 공유기라 칭하며 이를 통해 유선 LAN에 흐르는 신호를 무선 LAN 신호로 바꿔주어 신호가 닿는 범위 내에서 무선 인터넷을 이용할 수 있게 됩니다.
       - BSS(Basic Service Set)
         - BSS는 기본 서비스 집합을 의미하며 단순 공유기를 통해 네트워크에 접속하는 것이 아닌 동일 BSS 내에 있는 AP들과 장치들이 서로 통신이 가능한 구조를 말합니다.
         - 근거리 무선 통신을 제공하고, 하나의 AP만을 기반으로 구축이 되어 있어 사용자가 한 곳에서 다른 곳으로 자유롭게 이동하며 네트워크에 접속하는 것은 불가능합니다.
       - ESS(Extended Service Set)
         - ESS는 하나 이상의 연결된 BSS 그룹입니다. 장거리 무선 통신을 제공하며 BSS보다 더 많은 가용성과 이동성을 지원합니다.
         - 즉, 사용자는 한 장소에서 다른 장소로 이동하며 중단 없이 네트워크에 계속 연결할 수 있습니다.