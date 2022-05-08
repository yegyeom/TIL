## 세마포어 (Semaphore)

- 임계영역의 사용이 끝났으면 사용이 끝난 프로세스가 대기 중인 프로세스에게 끝났다는 사실을 알려주는 방식
- 시그널링을 통해 기다리는 프로세스를 잠재우고 깨우는 방식을 통해 busy-waiting을 하지 않게 한다.
- 현재 공유자원에 접근할 수 있는 스레드, 프로세스의 수를 나타내는 값을 두어 상호배제를 달성하는 기법
- 동기화 대상이 하나 이상

## 뮤텍스 (Mutex)

- 하나의 자원을 lock 매커니즘을 활용한 시그널링으로 관리한다.
- 락을 건 스레드만 락을 해제할 수 있다.
- 동기화 대상이 하나