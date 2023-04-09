# TLS/SSL handshake
- - -

<img width="600" src="https://cf-assets.www.cloudflare.com/slt3lc6tev37/5aYOr5erfyNBq20X5djTco/3c859532c91f25d961b2884bf521c1eb/tls-ssl-handshake.png">

    TLS는 인터넷 통신을 보호하기 위해 설계된 암호화 및 인증 프로토콜입니다. TLS 핸드셰이크는 TLS를 사용하는 통신 세션을 시작하는 과정입니다. 
    TLS 핸드셰이크 중에 두 통신 측은 서로를 인식하고 검증하며, 사용할 암호화 알고리즘을 설정하고 세션 키를 합의합니다. 
    TLS 핸드셰이크는 HTTPS가 작동하는 데 필수적인 구성 요소입니다.


## TLS handshake 중 발생하는 일

* 사용할 TLS 버전(TLS 1.0, 1.2, 1.3 등)을 지정합니다
* 사용할 암호 제품군(아래 참조)을 결정합니다
* 서버의 공개 키와 SSL 인증서 기관의 디지털 서명을 통해 서버의 ID를 인증합니다
* 핸드셰이크가 완료된 후에 대칭 암호화를 사용하기 위하여 세션 키를 생성합니다

## TLS/SSL handshake 과정

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9973E13B5C46B5B707">


1. SSL / TLS 클라이언트 컴퓨터가 자신의 버전, 암호 알고리즘 목록, 그리고 사용 가능한 압축 방식을 "client hello" 메시지에 담아 서버로 보냅니다.

2. SSL / TLS 서버는 클라이언트가 제공한 목록에서 서버가 선택한 암호 알고리즘, 선택한 압축 방식과 세션 ID 및 CA(Certificate Authority)가 사인한 서버의 공개 인증서를 "server hello" 메시지에 담아 응답합니다. 이 인증서는 대칭키가 생성되기 전까지 클라이언트가 나머지 handshake 과정을 암호화하는 데에 쓸 공개키를 담고 있습니다.

3. SSL / TLS 클라이언트는 서버의 디지털 인증서가 유효한지 신뢰할 수 있는 CA 목록을 통해 확인합니다.

4. 만약 CA를 통해 신뢰성이 확보되면 클라이언트는 의사 난수(pseudo-random) 바이트를 생성해 서버의 공개키로 암호화합니다. 이 난수 바이트는 대칭키를 정하는 데에 사용되며 이 대칭키는 나중에 메시지 데이터를 암호화하는 데 사용됩니다.

5. SSL / TLS 서버가 "클라이언트 인증서 요청"을 보낸 경우 클라이언트는 클라이언트의 디지털 인증서 또는 "디지털 인증서 없음 경고" 와 함께 클라이언트의 개인 키로 암호화 된 임의의 바이트 문자열을 보냅니다. 이 경고는 경고일 뿐이지만 일부 구현에서 클라이언트 인증이 필수일 경우 handshake 실패합니다.

6. 서버는 클라이언트의 인증서를 확인합니다. 난수 바이트를 자기 개인키로 복호화해 대칭 마스터키 생성에 활용합니다.

7. 클라이언트는 handshake의 클라이언트 부분이 완료되었음을 알리는 Finished 메시지를 서버에 보내면서 지금까지의 교환 내역을 해시한 값을 대칭키로 암호화하여 담습니다.

8. 서버는 스스로도 해시를 생성해 클라이언트에서 도착한 값과 일치하는지 봅니다. 일치하면 서버도 마찬가지로 대칭키를 통해 암호화한 Finished 메시지를 클라이언트에게 보냅니다.

9. 이후부터 SSL / TLS 세션 동안 서버와 클라이언트는 대칭키로 암호화된 어플리케이션(HTTP) 데이터를 주고 받을 수 있습니다.


## Reference

https://www.cloudflare.com/ko-kr/learning/ssl/what-happens-in-a-tls-handshake/

https://wangin9.tistory.com/entry/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%97%90-URL-%EC%9E%85%EB%A0%A5-%ED%9B%84-%EC%9D%BC%EC%96%B4%EB%82%98%EB%8A%94-%EC%9D%BC%EB%93%A4-5TLSSSL-Handshake