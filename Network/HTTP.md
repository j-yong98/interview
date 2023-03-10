HTTP
=
- HTTP는 애플리케이션 계층에서 웹서비스 통신에 사용됩니다. HTTP/1.0부터 발전을 거듭하여 현재 HTTP/3입니다.
- HTTP/1.0
  - HTTP/1.0은 기본적으로 한 연결당 하나의 요청을 처리하도록 설계 되었습니다. 이는 RTT 증가를 불러오게 되었습니다.
  - 서버로부터 파일을 가져올 떄마다 TCP의 3-way-handshake를 계속 열어야 하기 때문에 RTT가 증가하게 되는 단점이 있었습니다.
  - RTT의 증가를 해결하기 위한 방법
    - 매번 연결할 떄마다 RTT가 증가하니 서버에 부담이 많이 가고 사용자 응답 시간이 길어졌습니다. 이를 해결하기 위해 이미지 스플리팅, 코드 압축, 이미지 Base64 인코딩을 통해 사용하고 했습니다.
    - 이미지 스플리팅
      - 많은 이미지를 다운로드받게 되면 과부하가 걸리기 때문에 많은 이미지가 합쳐 있는 하나의 이미지를 다운로드받고, 이를 기반으로 background-image의 position을 이용하여 이미지를 표기하는 방법입니다.
    - 코드 압축
      - 코드 압축은 코드를 압축해서 개행 문자, 빈칸을 없애서 코드의 크기를 최소화하는 방법입니다.
    - 이미지 Base64 인코딩
      - 이미지 파일을 64진법으로 이루어진 문자열로 인코딩하는 방법입니다. 이 방법을 사용하면 서버와의 연결을 열고 이미지에 대해 서버에 HTTP 요청을 할 필요가 없다는 장점이 있습니다.
      - 하지만 Base64 문자열로 변환할 경우 37% 정도 크기가 더 커지는 단점이 있습니다.
###### RTT - 패킷이 목적지에 도달하고 나서 다시 출발지로 돌아오기까지 걸리는 시간이며 패킷 왕복 시간
###### 인코딩 - 정보의 형태나 형식을 표준화, 보안, 처리 속도 향상, 저장 공간 절약 등을 위해 다른 형태나 형식으로 변환하는 처리 방식
***
- HTTP/1.1
  - 매번 TCP를 연결하는 것이 아니라 한 번 TCP 초기화를 한 이후에 keep-alive라는 옵션으로 여러 개의 파일을 송수신 할 수 있게 바뀌었습니다.
  - HTTP/1.0에도 keep-alive가 있었지만 표준화가 되어 있지 않았고 HTTP/1.1부터는 표준화가 되어 기본 옵션으로 설정되었습니다.
  - 한 번 TCP 3-way-handshake가 발생하면 다음부터 발생하지 않지만 문서 안에 포함된 다수의 리소스를 처리하려면 요청할 리소스 개수에 비례해서 대기 시간이 길어지는 단점이 있습니다.
  - HOL Blocking
    - HOL Blocking(Head Of Line Blocking)은 네트워크에서 같은 큐에 있는 패킷이 그 첫번째 패킷에 의해 지연될 때 발생하는 성능 저하 현상을 말합니다.
  - HTTP/1.1의 헤더에는 쿠키 등 많은 메타데이터가 들어 있고 압축 되지 않아 무거웠습니다.
***
- HTTP/2
  - HTTP/2는 SPDY 프로토콜에서 파생된 HTTP/1.x보다 지연 시간을 줄이고 응답 시간을 더 빠르게 할 수 있으며 멀티플렉싱, 헤더 압축, 서버 푸시, 요청의 우선순위 처리를 지원하는 프로토콜입니다.
  - 멀티플렉싱
    - 멀티플렉싱이란 여러 개의 스트림을 사용하여 송수신한다는 것입니다. 이를 통해 특정 스트림의 패킷이 손실되었다고 하더라도 해당 스트림에만 영향을 미치고 나머지 스트림은 멀쩡하게 동작할 수 있습니다.
    - 스트림 : 시간이 지남에 따라 사용할 수 있게 되는 일련의 데이터 요소를 가르키는 데이터 흐름
    - 이를 통해 단일 연결을 사용하여 병렬로 여러 요청을 받을 수 있고 응답을 줄 수 있습니다. 이렇게 하여 HOL Blocking 문제를 해결할 수 있었습니다.
  - 헤더 압축
    - HTTP/2에서는 헤더압축을 써서 이전의 헤더 크기의 문제를 해결하였는데 허프만 코딩 압축 알고리즘을 사용하는 HPACK 압축 형식을 가집니다.
    - 허프만 코딩
      - 허프만 코딩은 문자열을 문자 단위로 쪼개 빈도 수를 세어 빈도가 높은 정보는 적은 비트를 써서 표현하고 빈도가 낮은 정보는 비트 수를 많이 사용하여 표현해 전체 데이터의 표현에 필요한 비트양을 줄이는 원리입니다.
  - 서버 푸시
    - HTTP/1.1에서는 클라이언트가 서버에 요청을 해야 파일을 다운로드받을 수 있었다면 HTTP/2는 클라이언트 요청 없이 서버가 바로 리소스를 푸시할 수 있게 되었습니다.
***
- HTTPS
  - HTTP/2는 HTTPS 위에서 동작합니다.
  - HTTPS는 애플리케이션 계층과 전송 계층 사이에 신뢰 계층인 SSL/TLS 계층을 넣은 신뢰할 수 있는 HTTP 요청을 말합니다. 이를 통해 '통신을 암호화'합니다.
  - SSL/TLS
    - SSL(Secure Socket Layer)은 SSL 1.0부터 시작해서 SSL 2.0, SSL 3.0, TLS(Transport Layer Security Protocol) 1.0, TLS 1.3까지 버전이 올라가며 마지막으로 TLS로 명칭이 변경되었으나 보통 SSL/TLS라고 부른다.
    - SSL/TLS은 전송 게층에서 보안을 제공하는 프로토콜입니다. 클라이언트와 서버가 통신할 때 SSL/TLS를 통해 제3자가 메시지를 도청하거나 변조하지 못하도록 합니다.
    - 공격자가 서버인 척하며 사용자 정보를 가로채는 네트워크상의 '인터셉터'를 방지할 수 있다.
    - 보안 세션을 기반으로 데이터를 암호화하며 보안 세션이 만들어질 때 인증 메커니즘, 키 교환 알고리즘, 해싱 알고리즘이 사용됩니다.
    - 보안 세션
      - 보안이 시작되고 끝나는 동안 유지되는 세션을 말하고, SSL/TLS는 핸드쉐이크를 통해 보안 세션을 생성하고 이를 기반으로 상태 정보 등을 공유합니다.
    - TLS 핸드쉐이크
      1. Client Hello (+ key share)
      2. Server Hello (+ key share)
         EncryptedExtensions
         Certificate
         CertificateVerify
         Finished
      3. Client Finish
      - 클라이언트와 서버가 키를 공유하고 이를 기반으로 인증, 인증 확인 등의 작업이 일어나는 단 한 번의 1-RTT가 생긴 후 데이터를 송수신하는 것을 볼 수 있습니다.
      - 클라이언트에서 사이퍼 슈트를 서버에 전달하면 서버는 받은 사이퍼 슈트의 암호화 알고리즘 리스트를 제공할 수 있는지 확인합니다.
      - 제공할 수 있다면 서버에서 클라이언트로 인증서를 보내는 인증 메커니즘이 시작되고 이후 해싱 알고리즘 등으로 암호화된 데이터의 송수신이 시작됩니다.
      - 사이퍼 슈트
        - 사이퍼 슈트는 프로토콜, AEAD 사이퍼모드, 해싱 알고리즘이 나열된 규약을 말합니다.
        - AEAD 사이퍼모드
          - AEAD(Authenticated Encryption with Associated Data)는 데이터 암호화 알고리즘이며 AES_128_GCM 등이 있습니다.
    - 인증 메커니즘
      - 인증 메커니즘은 CA(Certificate Authorities)에서 발급한 인증서를 기반으로 이루어집니다.
      - CA에서 발급한 인증서는 안전한 연결을 시작하는 데 있어 필요한 '공개키'를 클라이언트에게 제공하고 사용자가 접속한 '서버가 신뢰'할 수 있는 서버임을 보장합니다.
      - 인증서는 서비스 정보, 공개키, 지문, 디지털 서명 등으로 이루어져 있습니다.
      - CA는 아무 기업이나 할 수 있는 것이 아니고 신뢰성이 엄격하게 공인된 기업들만 참여할 수 있다.
      - CA 발급 과정
        - 자신의 서비스가 CA 인증서를 발급받으려면 자신의 사이트 정보와 공개키를 CA에 제출해야 합니다.
        - 이후 CA는 공개키를 해시한 값인 지문(finger print)을 사용하는 CA의 비밀키 등을 기반으로 CA 인증서를 발급합니다.
    - 암호화 알고리즘
      - 키 교환 암호화 알고리즘으로는 대수곡선 기반의 ECDHE(Elliptic Curve Diffie-Hellman Ephermeral) 또는 모듈식 기반의 DHE(Diffie-Hellman Ephermeral)를 사용합니다.
      - 둘 다 디피-헬만(Diffie-Hellman) 방식을 근간으로 만들어졌습니다.
      - 디피-헬만 키 교환 알고리즘
        - 디피-헬만 키 교환(Diffie-Hellman key exchange) 암호화 알고리즘은 암호키를 교환하는 하나의 방법입니다.
        - y = g^x mod p
        - 앞의 식에서 g와 x와 p를 안다면 y는 구하기 쉽지만 g와 y와 p만 안다면 x를 구하기는 어렵다는 원리에 기반한 알고리즘입니다.
        1. 처음에 공개 값을 공유하고 각자의 비밀 값과 혼합한 후 혼합 값을 공유합니다.
        2. 각자의 비밀 값과 또 혼합합니다. 공통의 암호키가 생성되는 것.
    - 해싱 알고리즘
      - 해싱 알고리즘은 데이터를 추정하기 힘든 더 작고, 섞여 있는 조각으로 만드는 알고리즘입니다. 
      - SSL/TLS는 해싱 알고리즘으로 SHA-256 알고리즘과 SHA-384 알고리즘이며 그 중 많이 쓰이는 알고리즘은 SHA-256 알고리즘입니다.
      - SHA-256
        - SHA-256 알고리즘은 해시 함수의 결과값이 256bit인 알고리즘이며 비트 코인을 비롯한 많은 블록체인 시스템에서도 씁니다.
        - SHA-256 알고리즘은 해싱을 해야 할 메시지에 1을 추가하는 등 전처리를 하고 전처리된 메시지를 기반으로 해시를 반환합니다.
  - HTTPS 구축 방법
    - 직접 CA에서 구매한 인증키를 기반으로 HTTPS 서비스를 구축하거나
    - 서버 앞단의 HTTPS를 제공하는 로드밸런서를 두거나 
    - 서버 앞단에 HTTPS를 제공하는 CDN을 둬서 구축합니다.
###### 세션 - 운영체제가 어떠한 사용자로부터 자신의 자산 이용을 허락하는 일정한 기간을 뜻한다. 즉, 사용자는 일정 시간동안 자원과 응용프로그램 등을 사용할 수 있다.
###### 개인키 - 비밀키라고도 하며, 개인이 소유하고 있는 키이자 반드시 자신만이 소유해야 하는 키
###### 공개키 - 공개되어 있는 키
###### 해시 - 다양한 길이를 가진 데이터를 고정된 길이를 가진 데이터로 매핑(mapping)한 값
###### 해싱 - 임의의 데이터를 해시로 바꾸어주는 일이며 해시 함수가 이를 담당
###### 해시 함수 - 임의의 데이터를 입력으로 받아 일정한 길이의 데이터로 바꿔주는 함수
***
- HTTP/3
  - HTTP/3은 HTTP/1.1 및 HTTP/2와 함께 World Wide Web에서 정보를 교환하는데 사용되는 HTTP의 세 번째 버전입니다.
  - TCP 위에서 돌아가는 HTTP/2와는 다르게 HTTP/3은 QUIC이라는 계층 위에서 돌아가며, TCP기반이 아닌 UDP 기반으로 돌아갑니다.
  - HTTP/2에서 장점이었던 멀티플렉싱을 가지고 있으며 초기 연결 설정 시 지연 시간 감소라는 장점이 있습니다.
  - 초기 연결 설정 시 지연 시간 감소
    - QUIC은 TCP를 사용하지 않기 때문에 통신을 시작할 때 번거로운 3-웨이 핸드쉐이크 과정을 거치지 않아도 됩니다.
    - QUIC은 첫 연결 설정에 1-RTT만 소요됩니다. 클라이언트가 서버에 어떤 신호를 한 번 주고, 서버도 거기에 응답하기만 하면 바로 본 통신을 시작할 수 있다는 것입니다.
    - QUIC은 순방향 오류 수정 메커니즘(FEC, Forward Error Correction)이 적용되었습니다. 이는 전송한 패킷이 손실되었다면 수신 측에서 에러를 검출하고 수정하는 방식이며 열악한 네트워크 환경에서도 낮은 패킷 손실률을 자랑합니다.