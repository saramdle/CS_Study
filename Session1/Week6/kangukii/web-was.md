# 웹서버와 WAS의 차이점

---

웹서버와 WAS의 차이점이 실제로 면접에서 자주 나오는 질문이라고 어디선가 들은거 같아서 이번 기회에 한번 정리를 해보려고 합니다.

이번 발표에서는 `정적페이지와 동적페이지`를 먼저 이해하고 그다음에 `둘의 차이점`에 대해서 알아보겠습니다.

### 1. 정적페이지와 동적페이지

#### 서론

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdxLCDa%2FbtrzpCYRjCs%2FiKOfAQJ5IkwWZ1MQOB4qHk%2Fimg.png" />

우리가 보는 웹페이지는 웹 서버에 주소(URL)을 가지고 통신 규칙(HTTP)에 맞게 요청을 하게 되면 알맞은 내용(HTML)을 응답받습니다.
하지만 이처럼 단순한 클라이언트(브라우저)와 웹서버로는 정적인 페이지만 처리하지 못한다는 한계점이 있습니다.

따라서 `정적인 HTML의 한계를 극복하고 동적인 페이지를 제공하고자 하는 목적, 더 나아가서 보안 강화와 장애 극복을 가능하게 하는 것이 WAS`입니다.

#### 본론

<img src="https://gmlwjd9405.github.io/images/web/static-vs-dynamic.png" style="background-color: white"/>

#### 1. 정적 페이지 (Static Page)

- 웹서버에서 파일 경로 이름을 받아서 경로와 일치하는 Content를 반환합니다.
- 항상 동일한 페이지를 반환합니다.
- 예를 들어 image, html, css, javascript 파일과 같이 컴퓨터에 저장되어 있는 정적 파일들을 말합니다.

#### 2. 동적 페이지 (Dynamic Page)

- 인자의 내용에 맞게 동적인 Content를 반환합니다.
- 웹서버에 의해 실행되는 프로그램을 통해 만들어진 결과물을 말합니다. (위의 사진에서 Servlet은 WAS 위에서 돌아가는 Java 프로그램을 말함)
- 개발자는 Servlet에 doGet()을 구현합니다. (doGet: GET 방식에서 호출되는 메서드, URL에 정보가 포함되어 보안에 약하고 기본 호출 메서드라고 합니다.) (Servlet: 동적처리가 가능한 서버 사이드에서 돌아가는 자바 프로그램)

<br>

### 2. Web Server와 WAS의 차이

<img src="https://gmlwjd9405.github.io/images/web/webserver-vs-was1.png" style="background-color: white"/>

#### Web Server

- Web Server의 개념
  - 소프트웨어와 하드웨어로 구분된다.
  - 하드웨어: Web 서버가 설치되어 있는 컴퓨터
  - 소프트웨어: `웹 브라우저 클라이언트로부터 HTTP 요청을 받아 정적인 컨텐츠(.html, .jpeg, .css 등)를 제공하는 컴퓨터 프로그램`
- Web Server의 기능
  - HTTP 프로토콜을 기반으로 해서 클라이언트의 요청을 서비스하는 기능을 담당합니다.
  - 요청에 따라 아래 두 가지 기능 중 적절하게 선택해서 수행합니다.
    - 기능 1)
      - 정적인 컨텐츠 제공
      - WAS를 거치지 않고 바로 자원을 제공한다.
    - 기능 2)
      - 동적인 컨텐츠 제공을 위한 요청 전달
      - 클라이언트의 요청을 WAS에 보내고 WAS가 처리한 결과를 클라이언트에게 전달한다.
      - (클라이언트는 일반적으로 웹 브라우저를 의미합니다.)
- 대표적인 Web Server의 예시
  - Apache Server, Nginx, IIS (Window 전용 Web 서버) 등

#### WAS (Web Application Server)

- WAS의 개념
  - DB조회나 다양한 로직 처리를 요구하는 동적인 컨텐츠를 제공하기 위해 만들어진 Application Server
  - HTTP를 통해 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어(소프트웨어 엔진)입니다.
- WAS의 역할
  - WAS = Web Server + Web Container
  - Web Server의 기능들을 구조적으로 분리시켜 처리하고자 하는 목적으로 제시되었습니다.
    - 분산 트랜잭션, 보안, 메시징, 쓰레드 처리 등의 기능을 처리하는 분산 환경에서 사용됩니다.
    - 주로 DB서버와 같이 수행됩니다.
  - 현재는 WAS가 가지고 있는 Web Server도 정적인 컨텐츠를 처리하는데 있어서 성능상 큰 차이가 없습니다.
- WAS의 주요 기능
  - 프로그램 실행 환경과 DB접속 가능 제공
  - 여러개의 트랜잭션 관리 기능
  - 업무를 처리하는 비즈니스 로직 수행
- WAS의 예시
  - Tomcat, JBoss, Jeus, Web Sphere 등

<br>

### 3. Web Server와 WAS를 구분하는 이유

#### Web Server가 필요한 이유?

- 이미지 파일과 같은 정적인 파일들은 웹문서가 클라이언트로 보내질 때 함께 가는 것이 아닙니다.
  - 클라이언트는 HTML 문서를 먼저 받고 그에 맞게 필요한 이미지 파일들을 다시 서버로 요청하면 그때서야 이미지 파일을 받아옵니다.
  - Web Server를 통해 정적인 파일들을 Application Server까지 가지 않고 앞단에서 빠르게 보내줄 수 있습니다.
- 따라서 Web Server에는 정적 컨텐츠만 처리하도록 기능을 분배해서 서버의 부담을 줄일 수 있습니다.

#### WAS가 필요한 이유는?

- 웹 페이지는 정적 컨텐츠와 동적 컨텐츠가 모두 존재합니다.
  - 사용자의 요청에 맞게 적절한 동적 컨텐츠를 만들어서 제공해야 합니다.
  - 이 때, Web Server만 이용하게 되면 사용자가 원하는 요청에 대한 결과값을 모두 미리 만들어 놓고 서비스를 제공해야 할겁니다.
  - 하지만 이렇게 서비스를 제공하기에는 자원이 너무나도 많이 부족합니다.
- 따라서 WAS를 통해 요청에 맞는 데이터를 DB에서 가져와서 비즈니스 로직에 맞게 그때그때 결과를 만들어서 제공함으로써 자원을 효율적으로 사용할 수 있습니다.

#### 그러면 WAS가 Web Server의 기능도 모두 수행하면 되는거 아닐까요?

- `기능을 분리해서 서버 부하 방지`
  - WAS는 DB 조회나 다양한 로직을 처리하느라 바쁘기 때문에 단순한 정적 컨텐츠는 Web Server에서 빠르게 클라이언트에 제공하는 것이 좋습니다.
  - WAS는 기본적으로 동적 컨텐츠를 제공하기 위해 존재하는 서버입니다.
  - 만약 정적 컨텐츠 요청까지 WAS가 처리한다면 정적 데이터 처리로 인해 부하가 커지게 되고, 동적 컨텐츠의 처리가 지연됨에 따라 수행 속도가 느려집니다. 그러면 페이지 노출 시간이 늘어나게 될 것입니다.
- `물리적으로 분리해서 보안 강화`
  - SSL에 대한 암복호화 처리에 Web Server를 사용
- `여러대의 WAS를 연결 가능`
  - Load Balancing을 위해 Web Server를 사용합니다.
  - 장애 처리에 유리합니다.
  - 특히 대용량 웹 어플리케이션의 경우(여러 개의 서버 사용) Web Server와 WAS를 분리하여 무중단 운영을 위한 장애 극복에 쉽게 대응할 수 있습니다.
  - 예를 들어, 앞 단의 Web Server에서 오류가 발생한 WAS를 이용하지 못하도록 한 후 WAS를 재시작함으로써 사용자는 오류를 느끼지 못하고 이용할 수 있다.

`결론적으로 자원 이용의 효율성 및 장애 극복, 배포 및 유지보수의 편의성을 위해 Web Server와 WAS를 분리한 것입니다. 추가적으로 Web Server를 WAS 앞에두고 필요한 WAS들을 Web Server에 플러그인 형태로 설정하면 더욱 효율적으로 분산처리가 가능합니다.`

<br>

### 4. Web Service Architecture

- Client -> Web Server -> DB
- Client -> WAS -> DB
- Client -> Web Server -> WAS -> DB

<img src="https://gmlwjd9405.github.io/images/web/web-service-architecture.png" style="background-color: white"/>

해당 사진은 대표적으로 사용하는 3번 구조의 동작 과정입니다. 참고해주시면 좋을 것 같습니다!

---

### Reference

- https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html
- https://helloworld-88.tistory.com/71
- https://code-lab1.tistory.com/199
