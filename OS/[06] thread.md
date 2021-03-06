# Thread

## 등장 배경

- 스레드가 없을 땐, fork 함수를 통해 각자의 분기를 타는 프로세스를 추가로 생성
- 예시 (채팅 프로그램)
  - 사용자가 입력하는 것을 처리하는 실행 path
  - 네트워크로부터 패킷이 도착하는 것을 처리하는 실행 path
- 문제
  - 프로세스는 각각 독립된 자원할당을 가짐 (서로 공유 X) => 서로에게 관련되지 않는 실행 path를 갖게됨
- 결론
  - 프로세스들 사이에서 통신이 발생
  - **어떤 방식이든 간에 IPC를 통해야하는 것**
  - 하지만, 프로그램이 커지고 시간이 지날 수록 매우 **비효율적**
  - 프로세스를 하나 만드는 것 = PCB를 만드는 것 = 실행할 메모리 공간을 별도로 만드는 것
  - 다른 프로세스와 통신 = 프로세스 간 context switching 발생 = 오버헤드 발생

### `프로세스 하나에 여러 흐름을 만들고 자원을 공유하자! => Thread`

## Thread

- 프로세스가 할당 받은 자원을 이용하는 실행 흐름의 단위
- Stack 영역만 따로 할당받고, 나머지 영역은 공유
- 각각의 스레드는 독립적인 작업을 수행해야 하기 때문에 각자의 Stack과 PC 레지스터 값을 가지고 있음

---

## 멀티 스레드

<img src="https://t1.daumcdn.net/cfile/tistory/995444505AD60F8314"></img>

- 장점
  1. 프로세스 내 자원들과 메모리를 공유하기 때문에 메모리 공간과 시스템 자원 소모가 줄어든다.
  2. 응답성이 증가한다.
- 단점
  1. 동기화 문제가 발생할 수 있다.
  2. 하나의 스레드에 문제가 생기면 전체 프로세스가 영향을 받는다.

---

## Reference

- https://jhnyang.tistory.com/368
- https://eun-jeong.tistory.com/20
