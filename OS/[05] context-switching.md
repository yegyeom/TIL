# Context Switching

## PCB (Process Control Block)

- 프로세스의 메타데이터를 저장해놓는 곳
- 하나의 PCB에는 하나의 프로세스 정보가 존재
- CPU에 급한 프로세스가 처리해달라고 긴급 요청이 온 경우, 기존 작업 프로세스를 어딘가에 임시 저장 해놓아야 급한 작업부터 처리한 후에 다시 불러올 수 있음 => **`즉, 프로세스 관한 정보들을 저장할 어딘가의 공간이 필요하다 => PCB`**

### PCB 저장 정보

1. OS가 관리상 사용하는 정보
   - Process state
   - Process ID
   - Priority
   - Scheduling information
2. CPU 수행 관련 하드웨어 값
   - Program Counter
   - Registers
3. 메모리 관련
   - Code, Data, Stack 위치 정보
4. 파일 관련
   - Open File Descriptors

---

## Context Switching

<img src="https://t1.daumcdn.net/cfile/tistory/994590345BB1B4DB2F"> <img/>

- 수행 중인(running) 프로세스 정보는 CPU 내부, 즉 레지스터에서 저장
- **CPU가 이전의 프로세스 상태를 PCB에 보관하고, 또 다른 프로세스의 정보를 PCB에서 읽어 레지스터에 적재하는 과정**
- 프로세스를 쭉 실행하면 될텐데 굳이 번거롭게 context switching 작업을 하는 이유?
  - 문맥교환을 안하고 기다리기만하면 CPU가 낭비됨
  - 전체적으로 봤을 때, overhead를 감수하더라도 문맥교환을 하는 것 (더 이득)
  - **CPU가 놀지 않고 사용자가 너무 기다리지 않게 관리하기 위해 context switching을 하는 것 => 이것이 운영체제가 하는 CPU 관리**

---

## Reference

- https://jhnyang.tistory.com/33
- https://developyo.tistory.com/198?category=752792
