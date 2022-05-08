# IPC (Inter-Process Communication)

- 협력 프로세스: 영향을 주고 받으며 자원을 공유하는 협력적인 프로세스
- 독립 프로세스: 다른 프로세스에서 영향을 끼치지도 받지도 않는 독립적인 프로세스
- **IPC: 협력 프로세스 사이에서 서로 데이터를 주고 받는 행위 또는 그에 대한 방법이나 경로**

### 1. Message passing

- 커널(OS)이 memory protection을 위해 **대리 전달**해주는 것
- 안전하고 동기화 문제가 없음
- 성능이 떨어진다. (큰 오버헤드)
- direct communication or indirect communication

### 2. Shared memory

- 두 프로세스간 **공유된 메모리**를 생성 후 이용하는 것
- 성능이 좋지만 동기화 문제 발생

#### `하나의 PC에서의 프로세스 통신 방법`

### 3. Socket

### 4. 원격 프로시저 호출 (RPC: Remote Procedure Call)

#### `Client-Server 관계인 다른 PC의 프로세스간 통신 방법`
