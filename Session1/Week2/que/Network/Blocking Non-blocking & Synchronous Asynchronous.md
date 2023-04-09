# Blocking I/O & Non-Blocking I/O & Synchronous & Asynchronous

<img src="https://developer.ibm.com/developer/default/articles/l-async/images/figure1.gif">

## Asynchronous blocking I/O

    블로킹 I/O가 구성되고, 그 다음 블로킹 select 시스템 호출을 사용하여 I/O 디스크립터에 대한 활동이 있는지 확인합니다. 
    select 호출을 흥미롭게 만드는 것은 하나의 디스크립터뿐만 아니라 여러 디스크립터에 대한 알림을 제공할 수 있다는 것입니다. 
    각 디스크립터에 대해 데이터 쓰기 능력, 읽을 데이터의 가용성, 그리고 오류가 발생했는지 여부를 알림 요청할 수 있습니다.

<img src="https://developer.ibm.com/developer/default/articles/l-async/images/figure4.gif">

    select 호출의 주요 문제점은 그 효율성이 매우 낮다는 것입니다. 
비동기식 알림을 위한 편리한 모델이지만, 고성능 I/O에 대한 사용은 권장되지 않습니다.

## Asynchronous non-blocking I/O (AIO)

    비동기식 논블로킹 I/O 모델은 I/O와 겹치는 처리 중 하나입니다. 읽기 요청은 즉시 반환되며, 읽기가 성공적으로 시작되었음을 나타냅니다. 
    백그라운드 읽기 작업이 완료될 때까지 애플리케이션은 다른 처리를 수행할 수 있습니다. 읽기 응답이 도착하면, 시그널 또는 스레드 기반 콜백을 생성하여 I/O 트랜잭션을 완료할 수 있습니다.

<img src="https://developer.ibm.com/developer/default/articles/l-async/images/figure5.gif">

    단일 프로세스에서 여러 개의 I/O 요청을 처리하면서 계산과 I/O 처리를 중첩시킬 수 있는 능력은 처리 속도와 I/O 속도 간의 차이를 이용합니다. 
    하나 이상의 느린 I/O 요청이 대기 중일 때, CPU는 다른 작업을 수행하거나 더 일반적으로 이미 완료된 I/O에서 작동할 수 있습니다.

## Reference

https://developer.ibm.com/articles/l-async/