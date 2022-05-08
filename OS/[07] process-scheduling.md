# 프로세스 스케줄링

- Ready Queue에 있는 프로세스들 중 실행시킬 프로세스를 하나 선택하는 것
- **고르는 작업: 스케줄링**
- **고른 프로세스를 CPU에 올리는 것: Dispath**

## Scheduling criteria

- 스케줄링 알고리즘이 일을 처리하는 데 있어서 좋다 나쁘다를 평가하는 기준

1. CPU Utilization (CPU 이용률)
   - CPU가 놀지 않고 얼마나 많이 사용되고 있는가
2. Throughput (처리율)

   - 단위 시간당 처리하는 일의 양
   - 주어진 시간 동안 몇 개의 프로세스를 수행했는가

3. Turnaround time (반환 시간)

   - 요청한 일을 수행한 시간
   - 작업 완료 시간 - 들어온 시간

4. Waiting time (대기 시간)

   - 일을 요청했는데 다른 프로세스가 실행되고 있어서 기다려야 하는 시간
   - running이 되기 위해 기다리는 시간
   - Turnaround time - burst time

5. Response time (응답 시간)

   - 첫 응답이 올 때까지 걸리는 시간
   - 처음 프로세스가 응답하는 시간 - 프로세스 도착 시간

#### `CPU Utilization, Throughput은 최대로, Turnaround time, Waiting time, Response time은 최소로`

## CPU Scheduling Algorithms

**1. FCFS (First-Come, First-Served)**

- 선입선출
- Non Preemption
- 간단하고 구현이 용이
- Convoy effect: 매우 오래 걸리는 프로세스가 할당될 경우, 다른 프로세스들의 대기 시간이 길어지는 현상

**2. SJF (Shortest-Job-First)**

- 짧은 작업 우선
- Non Preemption
- 실제로 적용하기 힘듦
  - 컴퓨터에서는 **프로세스가 어떤 CPU burst를 가지는지 CPU가 수행될 때에는 모른다.** -> I/O를 요청하는 명령어가 나와야 그때까지가 CPU burst이므로 미리 측정할 수 없다.
  - **즉, 프로세스가 얼마큼의 CPU burst를 가지는지 미리 알 수 없기에 실제로 적용하기 어려운 것.**

**3. SRT (Shortest Remaining Time)**

- 최소 잔여 시간 우선
- Preemption (SJF의 preemptive 한 버전)
- 실제로 적용하기 힘듦

**4. Priority Scheduling**

- 프로세스의 중요도를 기준으로 우선순위 부여
  - 내부적: 시간제한, 메모리 요구량, 열린 파일의 수, 평균 I/O burst 비율 등을 사용하여 우선순위 계산
  - 외부적: 외부적으로 이미 설정된 기준을 따름
- Non Preemption or Preemption
- 기아 현상 발생
  - 해결 방법: Aging (오래 기다릴수록 우선순위를 올림)

**5. Round-Robin**

- Time sharing 방식 이용 (FCFS의 preemptive version)
- Preemption (Time quantum 지나가면 다른 프로세스 실행)
- Time quantum의 크기를 정하는 것이 중요하다.
  - 작을 경우: Context Switching의 수가 늘어난다.
  - 극단적으로 클 경우: 프로세스의 크기만큼 CPU가 처리. 해당 프로세스가 끝나야 다른 프로세스가 처리됨 -> 결국 FCFS와 똑같음

**6. Multilevel Queue**

- 어떤 프로세스냐에 따라서 여러 종류의 그룹으로 나누고 여러 개의 큐에 다양한 알고리즘을 적용하는 기법
- 앞단의 프로세스들은 백그라운드에서 조용히 돌아가는 프로세스들보다 더 높은 우선순위를 갖게 됨 => 빠른 응답을 위해 당연히 다른 알고리즘이 적용되어야 더 효율적
- Foreground: Round-Robin
- Background: FCFS
- 큐 사이에 time-slice를 적용하는 방식도 존재 (각각 큐에게 다른 time quantum을 설정)
- 장점: 스케줄링 오버헤드가 낮음
- 단점: 한 번 해당 큐에 들어가면 프로세스는 다른 큐로 이동, 변경이 거의 불가능함 => 유연적이지 못함

**7. Multilevel Feedback Queue**

- 프로세스가 큐 사이 이동이 가능
  - 모든 프로세스는 하나의 입구로 진입
  - Time quantum을 다 채우지 못한 프로세스는 그대로 둠 (CPU burst가 작음)
  - Time quantum을 다 채운 프로세스는 그 밑의 레벨에 있는 큐로 이동 (CPU burst가 매우 큼)
  - 이때 특징은 밑에 있는 큐는 Time quantum 크기를 첫 번째 큐의 두 배로 돌린다.
  - 마지막 큐는 백그라운드 프로세스가 보통 그랬듯이 대게 FCFS로 처리된다.
- 장점
  - 유연성이 뛰어남
  - SJF 알고리즘처럼 turnaround 시간에 최적화되어있다. (짧은 프로세스를 먼저 돌게 해주므로 turnaround의 평균 시간을 줄일 수 있다.)
  - response time이 짧다. (Interactive 한 프로세스가 앞에 오므로)
- 단점: 기아 현상 발생
  - 해결 방안: Aging 방식 도입

---

## Reference

- 2020년도 숭실대학교 컴퓨터학부 운영체제 강의 (홍지만 교수님)
- https://jhnyang.tistory.com/8
- https://zzsza.github.io/development/2018/07/29/cpu-scheduling-and-process/
