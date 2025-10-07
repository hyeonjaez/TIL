## 아이템 81 - wait와 notify보다는 동시성 유틸리티를 이용하라


**wait/notify의 한계**

- 올바른 wait/notify 순서를 맞추기 어렵다
- 잘못된 시점에 Notify()를 호출하면 스레드가 영원히 깨어나지 않는다
- if 대신 while을 써야 하는데 실수하기 쉽다
- 어떤 스레드가 기다리는지 추적하기 어렵다

<br/>

**java.util.concurrent 유틸리티 사용**

1. 실행자 프레임워크 (Executor Framework)
  - 스레드를 직접 다루지 않고 태스크 단위로 실행을 관리하는 구조
  - Executor, ExecutorService는 스레드 생성과 관리의 책임을 분리해주고 wait/notify 없이도 자연스럽게 협력할수 있게 한다

2. 동시성 컬렉션
   - 동시에 접근해도 안전하게 동작하는 컬렉션들
   - ConcurrentHashMap, ConcurrentLinkedQueue 등등

3. 동시화 장치
  - 여러 스레드가 서로의 작업을 기다리거나 동시에 실행되도록 제어하는 장치들
  - CountDownLatch : 여러 스레드가 특정 개수의 이벤트가 끝날 때까지 대기
  - Semaphore : 동시에 접근 가능한 스레드 수 제한
  - CyclicBarrier : 스레드들이 동시에 특정 지점까지 도달해야 진행
  - Exchanger : 두 스레드 간 데이터 교환
  - Phaser : 단계별 협조를 위한 유연한 장치


<br/>

**만약 꼭 써야한다면**
- 표준 관용구를 따라라
- 항상 while 사용 -> 허위 깨움 대비
- wait는 synchronized 블록 안에서만 호출 가능
- notify 보다는 notifyAll을 사용 -> 누락된 스레드 방지
- 허위 깨움은 실제로 발생할수 있다 그래서 조건을 확인할때 반드시 while 루프를 사용해야 한다
