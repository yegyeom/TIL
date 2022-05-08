# 프로세스

- **프로그램**: 파일 시스템에 존재하는 실행 파일
- **프로세스**: 실행 중인 프로그램

## 프로세스

- **Code/Data/Stack/Heap**로 이루어진 구조의 메모리 영역을 할당 받음
- 프로세스는 최소 1개의 메인 스레드를 갖게 된다.
- 다른 프로세스의 자원에 접근하기 위해서는 [IPC](https://github.com/yegyeom/TIL/blob/main/OS/[04]%20ipc.md)를 사용해야 한다.

---

## 프로세스 메모리 구조

## <img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9c470866-5dfb-46bb-9ab6-ad049b0ec2e0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220508%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220508T061833Z&X-Amz-Expires=86400&X-Amz-Signature=dbdf1b3cbd3decd5911ae41a4131a5e2fdac580c54966758f4462b2195e50529&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject" />

- text (code segment)
  - 코드 데이터 (컴파일 된 코드)
  - 읽기 전용 영역
- data
  - 전역 변수, static 변수, 배열, 구조체 등
  - 프로그램이 실행될 때 생성되고 프로그램이 종료되면 시스템에 반환

```
code & data 영역
- 실행파일(.exe)에 존재
- 프로그램 시작시 RAM에 올라가면서 할당 됨.
```

- heap
  - 동적할당에 의해서 생기는 공간(c의 malloc, c++의 new)
  - 메모리 주소값에 의해서만 참조되고 사용되는 영역
  - 런타임에 크기를 알려줌으로써 영역을 확보하는 공간
- stack
  - 지역 변수나 매개 변수가 차지하는 공간
  - 함수 호출 시 생성되며, 함수가 끝나면 반환
  - 컴파일 타임에 크기가 결정됨

**Stack과 Heap영역은 사실 같은 공간을 공유한다. Heap은 메모리의 낮은 주소부터 할당되고 Stack은 높은 주소부터 할당된다. 이때 각 영역이 상대 공간을 침범하는 것을 각각 `stack overflow`, `heap overflow`라고 한다.**

---

## 프로세스 상태

<img src="https://camo.githubusercontent.com/acf5ebf3f753a000c78f552131f3b9b662de0829b06c13f91d37df29c43ea4c0/68747470733a2f2f696d67312e6461756d63646e2e6e65742f7468756d622f523132383078302f3f73636f64653d6d746973746f72793226666e616d653d6874747073253341253246253246626c6f672e6b616b616f63646e2e6e6574253246646e2532466456506d41332532466274714274394f774671762532463939745455794433706f4e6e6b316b6b314e7358696b253246696d672e706e67" />

- new: 프로세스가 만들어지는 과정
- running: CPU에서 수행 되고 있는 상태
- ready: 메모리 등 다른 조건을 모두 만족하는 상태에서 CPU를 기다리는 상태
- waiting
  - CPU를 주어도 당장 수행할 수 없는 상태
  - 프로세스 자신이 요청한 event가 즉시 만족되지 않아 이를 기다리는 상태
  ```
  [예시 - 게임]
  - running 상태로 게임을 진행하다가 로그인을 해야만 진행 가능
  - CPU는 사용자로부터 ID와 PW를 받을 때까지 수행하지 못함 => 그동안 CPU가 아무 것도 안하는 것은 큰 낭비
  - 따라서 CPU는 작업을 waiting 상태로 바꿔버리고 다른 프로세스를 가져와서 running으로 돌려 놓음
    (ready 상태인 다른 프로세스가 running 상태가 되는 것)
  - 이처럼 내 스스로 더 이상 수행이 안되어서 어떤 이벤트(I/O)가 발생하기를 기다리는 상태 => waiting
  - 사용자가 입력을 완료하면 waiting 상태였던 프로세스가 CPU에게 인터럽트 신호를 줌
  - 다시 실행할 모든 준비가 되었으므로 I/O or event completion가 돼서 waiting에서 ready로 상태 변경
  ```
- swap-out (suspend): 메모리를 강제로 뺏긴 상태 (종료되지 않은 프로세스의 전체 이미지 또는 일부를 주기억장치로부터 스왑 공간으로 이동 시키는 것)
- terminated: 수행이 끝난 상태

---

## 멀티 프로세스

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FApUCF%2FbtqBD1a0SBH%2Fi05f8OsvEVM1gayzod7HRK%2Fimg.png" width="80%" alt="img"></img>

- 장점
  1. 하나의 프로세스가 죽더라도 다른 프로세스에 영향을 주지 않는다. (안정성이 높음)
- 단점
  1. 독립된 메모리 영역이므로 작업량이 많을 수록 오버헤드가 발생하여 성능저하가 발생할 수 있다.
  2. 멀티 스레드보다 많은 메모리 공간과 CPU 시간을 차지한다.

---

## Reference

- https://jhnyang.tistory.com/32
- https://kyu9341.github.io/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C/2020/10/04/OS_Process_Structure/
- https://jhnyang.tistory.com/7
- https://developyo.tistory.com/198?category=752792
- 2020년도 숭실대학교 컴퓨터학부 운영체제 강의 (홍지만 교수님)
