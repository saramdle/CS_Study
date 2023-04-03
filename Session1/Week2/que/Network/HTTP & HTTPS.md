# HTTP & HTTPS
- - -

## HTTP

    HTTP(HyperText Transfer Protocol)는 하이퍼 텍스트 전송 프로토콜으로 간단히 말해서 인터넷을 작동시키는 역할을 하며, 
    웹 서버 및 웹 브라우저 상호 간의 데이터 전송을 위한 응용계층 프로토콜입니다.
    
    웹 사이트에 액세스하기 위해서는 프로토콜 변형이 필요한데, 이때 웹 사이트 URL이 일반적으로 “http://...”로 시작하며 
    URL에 해당하는 웹 페이지를 가져오기 위해 웹 사이트 서버에 명령을 보내 작동하게 됩니다.

### HTTP/1.0

HTTP/1.0은 기본적으로 한 연결당 하나의 요청을 처리하도록 설계되었습니다. 이는 RTT 증가를 불러오게 되었습니다.


(RTT란 패킷이 목적지에 도달하고 나서 다시 출발지로 돌아오기까지 걸리는 시간)

<img width="600" src="https://velog.velcdn.com/images/ljw4536/post/54816c33-fea5-4f8a-aa2c-83d8f5eb7d93/image.png">

서버로부터 파일을 가져올 때머다 TCP의 3-웨이 핸드셰이크를 계속해서 열어야 하기 때문에 RTT가 증가하는 단점이 있었습니다.

### HTTP/1.1

HTTP/1.0에서 발전한 것이 바로 HTTP/1.1입니다. 매번 TCP 연결을 하는것이 아니라 한 번 TCP 초기화를 한 이후에 keep-alive라는 옵션으로 여러 개의 파일을 송수신할 수 있게 바뀌었습니다. 

참고로 HTTP/1.0에서도 keep-alive가 이었지만 표준화가 되어 있지 않았다.

<img width="600" src="https://user-images.githubusercontent.com/40616436/79342851-9d439600-7f68-11ea-9a1c-80782d6cbb6e.png">

그림처럼 한 번 TCP 3-웨이 핸드셰이크가 발생하면 그 다음부터 발생하지 않는 것을 볼 수 있습니다. 하지만 문서 안에 포함된 다수의 리소스를 처리하려면 요청할 리소스 개수에 비례해서 대기 시간이 길어지는 단점이 있습니다.

* **HOL Blocking**
    
<img width="500" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile1.uf.tistory.com%2Fimage%2F26040A41593815B020B6F5">


HOL Blocking(Head Of Line Blocking)은 네트워크에서 같은 큐에 있는 패킷이 그 첫 번째 패킷에 의해 지연될 때 발생하는 성능 저하 현상

### HTTP/2

HTTP/2는 SPDY 프로토콜에서 파생된 HTTP/1.x보다 지연 시간을 줄이고 응답 시간을 더 빠르게 할 수 있으며 **멀티플렉싱, 헤더 압축, 서버 푸시**, 요청의 우선순위 처리를 지원하는 프로토콜입니다.

* **멀티플렉싱**

<img width="500" src="https://ssup2.github.io/images/theory_analysis/HTTP2/HTTP2_Frame_interleaving.PNG">

멀티플렉싱이란 여러 개의 스트림을 사용하여 송신한다는 것입니다. 

(스트림이란 시간이 지남에 따라 사용할 수 있게 되는 일련의 데이터 요소를 가리키는 데이터 흐름)

* **헤더 압축**

<img width="500" src="https://ssup2.github.io/images/theory_analysis/HTTP2/HTTP2_Header_Compression.PNG">

HTTP/1.x에는 크기가 큰 헤더라는 문제가 있었습니다. 이를 HTTP/2에서는 헤더 압축을 써서 해결하는데, 허프만 코딩 압축 알고리즘을 사용하는 HPACK 압축 형식을 가집니다.

* **서버 푸시**

<img width="500" src="https://ssup2.github.io/images/theory_analysis/HTTP2/HTTP2_Server_Push.PNG">

HTTP/1.1에서는 클라이언트가 서버에 요청을 해야 파일을 다운로드받을 수 있었다면, HTTP/2는 클라이언트 요청 없이 서버가 바로 리소스를 푸시할 수 있습니다.

## HTTPS

    HTTP/2는 HTTPS 위에서 동작합니다. HTTPS는 애플리케이션 계층과 전송 계층 사이에 
    신뢰 계층인 SSL/TLS 계층을 넣은 신뢰할 수 있는 HTTP 요청을 말합니다. 이를 통해 '통신의 암호화'합니다.

* **SSL/TLS**

SSL/TLS는 전송 계층에서 보안을 제공하는 프로토콜입니다. 클라이언트와 서버가 통신할 때 SSL/TLS를 통해 제 3자가 메시지를 도청하거나 변조하지 못하도록 합니다.

<img width="500" src="https://blog.kakaocdn.net/dn/dLpa9j/btrnqx2LpIV/hKTqMkQDLtQdOiv39j7KPk/img.png">

SSL/TLS를 통해서 공격자가 서버인 척하며 사용자 정보를 가로채는 네트워크상의 '인터셉터'를 방지할 수 있습니다.

* **인증 메커니즘**

인증 메커니즘은 CA(Certificate Authorities)에서 발급한 인증서를 기반으로 이루어 집니다. 

CA에서 발급한 인증서는 안전한 연결을 시작하는 데 있어 필요한 '공개키'를 클라이언트에 제공하고 사용자가 접속한 '서버가 신뢰'할 수 있는 서버임을 보장합니다.

* **HTTPS 구축방법**

HTTPS 구축 방법은 크게 세 가지입니다. 직접 CA에서 구매한 인증키를 기반으로 HTTPS 서비스를 구축하거나, 서버 앞단의 HTTPS를 제공하는 로드밸런서를 두거나, 서버 앞단에 HTTPS를 제공하는 CDN을 둬서 구축합니다.