# TCP 3 Way-Handshake & 4 Way-Handshake
- - -

    3-Way Handshake 는 TCP의 접속,4-Way Handshake는 TCP의 접속 해제 과정이다.

## TCP 3 Way-Handshake

    TCP 통신을 이용하여 데이터를 전송하기 위해 네트워크 연결을 설정(Connection Establish) 하는 과정
    양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이터 전달이 시작하기 전에 한 쪽이 다른 쪽이 준비되었다는 것을 알 수 있도록 한다.
    즉, TCP/IP 프로토콜을 이용해서 통신을 하는 응용 프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다.

<img width="500" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F225A964D52F1BB6917">

1. A클라이언트는 B서버에 접속을 요청하는 SYN 패킷을 보낸다. 이때 A클라이언트는 SYN 을 보내고 SYN/ACK 응답을 기다리는SYN_SENT 상태가 되는 것이다.
2. B서버는 SYN요청을 받고 A클라이언트에게 요청을 수락한다는 ACK 와 SYN flag 가 설정된 패킷을 발송하고 A가 다시 ACK으로 응답하기를 기다린다. 이때 B서버는 SYN_RECEIVED 상태가 된다.
3. A클라이언트는 B서버에게 ACK을 보내고 이후로부터는 연결이 이루어지고 데이터가 오가게 되는것이다. 이때의 B서버 상태가 ESTABLISHED 이다.

위와 같은 방식으로 통신하는것이 신뢰성 있는 연결을 맺어 준다는 TCP의 3 Way handshake 방식이다.

## TCP 4 Way-Handshake

    4-Way Handshake은 연결을 해제 (Connecntion Termination)하는 과정이다.

<img width="500" src="https://velog.velcdn.com/images%2Faverycode%2Fpost%2F3ec34c06-3d54-45f3-a6fb-bc5bfb415001%2F%E1%84%80%E1%85%B5%E1%84%89%E1%85%AE%E1%86%AF%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8-6%202.jpg">

1. 클라이언트는 서버에게 연결을 종료한다는 FIN 플래그를 보낸다. (`FIN` (finish) : 세션을 종료시키는데 사용되며, 더 이상 보낸 데이터가 없음을 나타낸다.)
2. 서버는 FIN을 받고, 확인했다는 ACK를 클라이언트에게 보낸다. (이때 모든 데이터를 보내기 위해 CLOSE_WAIT 상태가 된다)
3. 데이터를 모두 보냈다면, 연결이 종료되었다는 FIN 플래그를 클라이언트에게 보낸다.
4. 클라이언트는 FIN을 받고, 확인했다는 ACK를 서버에게 보낸다. (아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT을 통해 기다린다.)
   * 서버는 ACK를 받은 이후 소켓을 닫는다 (Closed)
   * TIME_WAIT 시간이 끝나면 클라이언트도 닫는다 (Closed)


## Reference

https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake

https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake