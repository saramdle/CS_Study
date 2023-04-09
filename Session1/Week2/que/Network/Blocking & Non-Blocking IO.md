# Blocking I/O & Non-Blocking I/O
- - -

## Blocking I/O


    Blocking I/O는 I/O 작업이 완료될 때까지 호출한 함수가 반환되지 않고 대기하며, 이를 동기적 작업(Synchronous operation)이라고 합니다.
    대표적인 Blocking I/O 함수로는 read(), write(), accept() 등이 있습니다.

<img src="https://grip.news/wp-content/uploads/2019/06/bio_01.gif">

    read()를 호출해 kernel에 read I/O를 요청하면, read가 끝날 때가지 application은 block이 되어 다른 read response가 올때까지 다른 작업을 수행할 수 없다.

<span style="font-size: 20px">**⭐️ Blocking I/O 장점**</span> <br>

1. 쉬운 사용법: 함수 호출 결과를 바로 반환하여 쉽게 이해할 수 있습니다.
2. 프로그래밍이 단순합니다: 동기적으로 호출하기 때문에 코드 작성이 간단합니다.
3. 운영체제와의 상호작용이 적습니다: Blocking I/O 함수는 운영체제와의 상호작용이 적기 때문에 운영체제의 자원을 적게 사용합니다.

<br>

<span style="font-size: 20px">**💀️ Blocking I/O 단점**</span> <br>

1. 성능이 떨어집니다: I/O 작업이 완료될 때까지 대기하기 때문에, 다른 작업을 수행하지 못하고 기다려야 합니다.
2. Scalability 문제가 발생합니다: 동기적으로 작업을 처리하기 때문에, 클라이언트가 많아지면 처리 속도가 느려지는 문제가 발생합니다.

<br>

## Non-Blocking I/O

    Non-Blocking I/O는 I/O 작업이 완료될 때까지 `대기하지 않고 다른 작업을 수행`할 수 있는 작업 형태를 `비동기적 작업(Asynchronous operation)`이라고 합니다. 
    Non-Blocking I/O는 I/O 작업을 요청하고, 결과를 기다리지 않고 바로 다른 작업을 수행할 수 있으며, I/O 작업이 완료되면 알림을 받아 처리합니다.

<img src="https://grip.news/wp-content/uploads/2019/06/bio_02.gif">

    read I/O를 하기 위해서 kernel에 요청을 하면 작업을 완료 여부와 관계없이 즉시 응답을 하여 CPU 제어권을 다시 application에 넘겨준다.
    

<span style="font-size: 20px">**⭐️ Non-Blocking I/O 장점**</span> <br>

1. 높은 성능: 다른 작업을 수행하면서 I/O 작업도 처리할 수 있으므로, 전체적인 처리량(Throughput)이 높아집니다.
2. Scalability가 높습니다: Non-Blocking I/O 함수는 하나의 스레드로 여러 클라이언트를 동시에 처리할 수 있습니다.
3. 대기 시간이 적습니다: I/O 작업이 완료될 때까지 대기하지 않으므로, 전반적인 대기 시간이 적어지고 응답 시간이 빨라집니다.

<br>

<span style="font-size: 20px">**💀️ Non-Blocking I/O 단점**</span> <br>

1. 복잡한 구현: 비동기적 작업이므로, 처리 결과를 대기하지 않고 알림을 받아 처리하는 방식이 필요합니다. 이러한 방식을 구현하기 위해서는 상태를 관리하는 복잡한 코드가 필요합니다.
2. 운영체제와의 상호작용이 많아집니다: Non-Blocking I/O 함수는 운영체제와 더 자주 상호작용하므로, 운영체제의 자원을 더 많이 사용합니다.
3. 코드 복잡도가 높습니다: I/O 작업이 완료되었을 때 호출할 콜백 함수를 작성해야 하므로, 코드 복잡도가 높아집니다.
4. 오버헤드가 큽니다: Non-Blocking I/O에서는 I/O 작업이 완료되었을 때 콜백 함수를 호출해야 하므로, 호출 오버헤드가 발생합니다. 이러한 오버헤드는 작은 I/O 작업에 대해서는 부담이 적지만, 큰 I/O 작업에 대해서는 부담이 크게 됩니다.

<br>