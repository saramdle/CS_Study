# ✏️ TCP 3-4 way Handshake

---

TCP handshake 과정은 TCP의 신뢰성있는 통신 연결을 성립하고 해제하는 과정을 말합니다. <br>
설명에 들어가기 전에 간단하게 TCP가 무엇인지 설명을 드리고 진행을 해보겠습니다.

<br>

### 1. TCP란? (Transmission Control Protocol)

TCP는 인터넷상에서 데이터를 메세지의 형태로 보내기 위해 IP와 함께 사용하는 프로토콜입니다. 주로 애플리케이션에게 신뢰적이고 연결지향성 서비스를 제공하고 있습니다.

결론적으로 **서버와 클라이언트간에 데이터를 신뢰성있게 전달하기 위해 만들어진 프로토콜**입니다.

<br>

### 2. State 정보와 Flag 정보

#### State 정보

- `CLOSED`: 닫힌 상태입니다. 즉, 데이터를 주고 받기 전 연결이 안된 기본 상태를 말합니다.
- `CLOSE-WAIT`: 서버 측에서 클라이언트로 부터 연결을 해제하겠다 신호를 받은 상태이며, 아직 전송이 끝날 때까지 대기하는 상태입니다. 이러한 대기하는 상태는 전송이 끝나지 않은 데이터의 손실을 예방해줍니다.
- `LISTEN`: 포트가 열린 상태로 연결 요청을 대기하는 중입니다. 즉, CLOSED 상태에 있던 서버가 데이터를 받을 준비가 되어 대기하는 상태를 의미합니다.
- `SYN_RECEIVED`: 클라이언트 측에서 보낸 SYN을 서버 측에서 잘 받았다는 상태를 의미합니다.
- `SYN-SENT`: 클라이언트 측에서 SYN을 보냈다는 상태로, 이 말은 다른 말로 서버측의 응답을 기다리고 있는 상태를 의미합니다.
- `ESTABLISHED`: 연결이 성공적으로 된 상태를 의미합니다. 클라이언트 측에선 서버의 응답을 받으면 해당 상태가 되고, 서버 측에선 응답을 보내고 다시 클라이언트 측에서 데이터를 보내면 해당 상태가 됩니다.
- `FIN-WAIT`: 클라이언트 측에서 서버에 연결을 해제하겠다고 신호를 보낸 상태를 의미합니다.
- `TIME-WAIT`: Server로 부터 FIN을 수신하더라도 일정시간동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정을 말합니다.
- `LAST-ACK`: 서버 측에서 전송이 끝나고 클라이언트 측으로 전송이 완전히 끝났다는 신호를 보낸 상태입니다

#### Flag 정보

- **TCP Header에는 CONTROL BIT(플래그 비트, 6bit)가 존재하고, 각 bit는 'URG-ACK-PSH-RST-SYN-FIN'의 의미를 가집니다.**

  - 즉, 해당 위치의 bit가 1이면 해당 패킷이 어떤 내용을 담고있는 패킷인지 나타냅니다.

- **SYN (Synchronize Sequence Number)**

  - 연결 설정. Sequence Number를 랜덤으로 설정하여 세션을 연결하는데 사용하고 초기에 Sequence Number를 전송합니다.
  - Connection을 위한 Flag.
  - **다시 말해서, 3-Way Handshake에서 연결을 위해 특정 숫자를 보낸다고 말씀드렸는데 여기서 특정 숫자를 `Sequence Number(SYN)`이라고 합니다.**

- **ACK (Acknowledgement)**

  - 응답 확인. 패킷을 받았다는 것을 의미하는 Flag.
  - ACK도 특정 숫자로 이루어져 있는데 보통 SYN이 보낸 숫자에 +1을 한 값입니다.

- **FIN (Finish)**

  - 연결을 종료시킬 때 사용됩니다.
  - 4-Way Handshake에서 사용됩니다.

<br>

### 2. TCP 3-Way Handshake

> TCP/IP 프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정입니다.

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcolneJ%2FbtrEE0Ggbwx%2FVzhD9eByIMPCRSn6QSGGy1%2Fimg.png" />

3-Way Handshake는 양쪽 모두 데이터를 전송할 준비가 되어있다는 것을 보장하고 실제로 데이터 전달이 시작하기 전에 다른 한쪽이 준비되었다는 것을 알 수 있도록 해줍니다.

#### 3-Way Handshake 동작 방식

**1️⃣ Client -> SYN -> Server (전화 들려?)**

Client가 Server에게 접속을 요청하는 `SYN(X)`을 보냅니다. 송신자가 최초로 데이터를 전송할 때 Sequence Number를 난수(X)로 지정하고 SYN 플래그 비트를 1로 설정한 세그먼트를 전송합니다.<br>

**Client는 CLOSED에서 `SYN-SENT`로 상태변경이 됩니다.**

**2️⃣ Server -> SYN + ACK -> Client (응 들리는디 너는?)**

Server는 `LISTEN` 상태에서 클라이언트로부터 `SYN(X)`이 들어온 것을 확인하고 요청을 수락한다는 `ACK과 SYN Flag(SYN(Y) + ACK(X+1))`가 설정된 패킷을 발송하고 클라이언트로부터 ACK이 오길 기다립니다. 이 때 Server는 `SYN_RECEIVED` 상태로 바뀌게 됩니다.

**3️⃣ Client -> ACK -> Server (나도 들려! 이제 말할게)**

Client에서는 Server로부터 `SYN(Y)+ACK(X+1)` 패킷을 받고 `ESTABLISHED` 상태가 됩니다. 그리고 Server로 `ACK(Y+1)`을 보내게 됩니다.

Server는 Client로부터 `ACK(Y+1)`을 받게 되고 마찬가지로 `ESTABLISHED` 상태가 되고 Client와 Server간의 연결이 이루어지게 됩니다.

<br>

`위와 같이 신뢰성을 위해 3번의 핸드쉐이킹을 거쳐 연결을 맺는 것을 3-Way Handshake라고 합니다.`

<br>

### 3. TCP 4-Way Handshake

> 3-Way는 연결확립을 위해 진행을 했다면 4-Way는 세션을 종료하기 위해 수행되는 절차를 의미합니다.

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ft6DvO%2FbtrEDRCPzv1%2FOZkk7v80ZeXxftjCrOE710%2Fimg.png" />

#### 4-Way Handshake 동작 방식

**1️⃣ Client -> FIN -> Server (나 이제 전화 끊고싶어!)**

Server와 Client가 연결된 상태에서 Client가 연결을 종료하겠다는 `FIN 플래그`를 Server에 전송합니다. 보낸후에 State를 `FIN-WAIT-1` 상태로 변환합니다.

참고로 이 1번 과정에서 FIN 패킷에는 실질적으로 ACK이 포함되어 있다고 합니다. 이는 `Half-Close` 기법때문이라고 합니다.

> - 연결을 종료하려고 할 때 완전히 종료하지 않고 반만 종료합니다.<br>
> - Half-close 기법을 사용하게 되면 종료 요청자가 처음 보내는 FIN 패킷에 승인 번호를 함께 담아서 보내게 되는데 이 때 승인 번호의 의미는 "일단 연결은 종료할건데 귀는 열어둘게. 이 승인 번호까지 처리했으니까 더 보낼 거 있으면 보내!"가 됩니다.
> - 이후 수신자가 남은 데이터를 모두 보내고 나면 다시 요청자에게 FIN 패킷을 보냄으로써 모든 데이터가 처리되었다는 신호인 FIN을 보내게 됩니다. 여기서 FIN은 그림에서 서버가 보내는 FIN을 의미합니다. 그렇게 되면 요청자는 나머지 반을 닫으면서 좀 더 안전하게 연결을 종료할 수 있게 됩니다.

**2️⃣ Server -> ACK -> Client (오키! 그러면 나 이거까지만 말하고 끊을게)**

`FIN 플래그`를 받은 Server는 확인메세지인 `ACK`을 Client에 보내고 자신(Server)의 통신이 끝날때까지 기다리게 됩니다. 이 상태가 `CLOSE-WAIT`입니다. Client도 마찬가지로 Server에서 종료될 준비가 됐다는 `FIN`을 받기 위해 `FIN-WAIT-2` 상태로 변환합니다.

**3️⃣ Server -> FIN -> Client (이제 다 말했어! 끊자~)**

Server에서 작업이 모두 끝나고 Client에게 `FIN`을 전송합니다.

**4️⃣ Client -> ACK -> Server (오키 알았어~)**

Client는 `FIN`을 받고 해지 준비가 되었다는 정상응답인 `ACK`을 Server에게 보내준다. 이 때 Client는 `TIME-WAIT` 상태로 변경된다. 여기서 TIME-WAIT 상태는 `의도치 않은 에러로 인해 연결이 데드락으로 빠지는 것을 방지`하기 위해 변경되는 것인데 만약 에러로 인해 종료가 지연되다가 타임이 초과되면 CLOSED 상태로 변경됩니다.

예를 들어보겠습니다. 만약 Server에서 FIN을 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN보다 늦게 도착하는 상황이 발생한다면 어떻게 될까요?

Client에서는 연결을 종료시킨 후 뒤늦게 도착하는 패킷이 있다면 이 패킷은 Drop되고 데이터는 유실될 것입니다.

이러한 현상에 대비하여 Client는 Server로부터 FIN을 수신하더라도 일정시간(Default는 240초) 동안 연결을 남겨놓고 잉여 패킷을 기다리는 과정을 거치게 되는데 이 과정을 `TIME_WAIT` 라고 합니다.

<br>

`이후 서버는 ACK을 받고 CLOSED 상태로 들어가서 소켓을 닫게 되고, TIME-WAIT 시간이 끝나면 클라이언트도 CLOSED 상태가 됩니다.`

<br>

### 4. 자주 나오는 기술면접 질문 정리

#### (1) TCP의 연결 설정 과정(3단계)와 연결 종료 과정(4단계)이 단계가 차이나는 이유는 무엇인가요?

> Client가 데이터 전송을 마쳤다고 하더라도 Server는 아직 보낼 데이터가 남아 있을수도 있습니다. 따라서 일단 FIN에 대한 ACK만 보내고 데이터를 모두 전송한 후에 자신도 FIN 메세지를 보내기 때문입니다.

#### (2) 만약 Server에서 FIN 플래그를 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN 패킷보다 늦게 도착하는 상황이 발생하면 어떻게 될까요?

> TCP에서는 이러한 현상에 대비해서 Client는 Server로부터 FIN 플래그를 수신하더라도 일정시간동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정을 거친다고 합니다.

#### (3) 초기 Sequence Number인 ISN(Initial Sequence Number)을 0부터 시작하지 않고 난수를 생성해서 설정하는 이유는?

> Connection을 맺을 때 사용하는 포트번호는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용됩니다. 따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용하는 가능성이 존재하게 됩니다. 서버측에서는 패킷의 SYN을 보고 패킷을 구분하게 되는데 난수가 아닌 순차적인 번호를 전송하게 된다면 이전의 Connection으로부터 오는 패킷으로 인식할 수 있습니다. 따라서 이런 문제가 발생할 가능성을 줄이기 위해 난수로 ISN을 설정합니다.

---

## Reference

- https://jeongkyun-it.tistory.com/180
- https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake
- https://www.geeksforgeeks.org/tcp-3-way-handshake-process/
- https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake
