# 메모리 관리

- MMU (Memory management unit): CPU 코어 안에 탑재되어 **가상 주소를 실제 메모리 주소로 변환해 주는 장치**

## 연속 메모리 할당 (Contiguous Allocation)

- 각각의 프로세스가 메모리의 연속적인 공간에 적재
- 논리적 주소가 연속적이면 물리적 주소도 연속적으로 배치된다.
- 현재는 사용하지 않는 방식
- 장점: MMU가 간단 (덧셈, 비교)
- 단점: 단편화

1. 고정 분할 방식

   - 물리적 메모리를 몇 개의 영구적 분할로 나눈다.
   - 분할당 하나의 프로그램을 적재
   - 내부/외부 단편화 발생

2. 가변 분할 방식

   - 프로그램 크기를 고려해서 할당
   - 분할의 크기, 개수가 동적으로 변함
   - 외부 단편화 발생
     - Compaction으로 해결하려 했으나 비효율적, 실행 가능성이 낮음
   - Hole
     - 가용 메모리 공간
     - 프로세스가 도착하면 수용 가능한 Hole을 할당
   - Hole 관리 방법 (현재 프로세스가 어떤 공간에 들어가는 게 효율적인지에 대한 전략)

     **1. First-Fit (최초 적합)**

     - 가장 최초로 발견되는 hole에 할당하는 방법

     **2. Best-Fit (최적 적합)**

     - 가장 잘 맞는 곳에 할당 (가급적이면 자투리를 조그맣게)

     **3. Worst-Fit (최악 적합)**

     - 가장 큰 공간에 할당
     - 자투리를 크게 만들어야 또 다른 프로세스가 남은 자투리에 들어갈 수 있으므로 (2번과 반대 사고)

     ### **`어떤 전략이든 외부 단편화는 발생함`**

---

## 비연속 메모리 할당 (Noncontiguous Allocation)

- 하나의 프로세스가 메모리의 여러 영역에 분산되어 올라감

**1. Paging (페이징)**

- **프로세스를 일정 크기인 페이지로 잘라서 메모리에 적재하는 방식**
- 논리적 주소와 물리적 주소를 동일한 크기로 자른 후 알맞게 배치 (고정 분할)
- 하나의 프로세스를 굳이 연속적으로 배치할 필요가 없다. => 자투리 공간이 발생하지 않는다. **`=> 외부 단편화가 절대 발생하지 않는다.`**
- Page table은 메인 메모리에 상주
- Page table 사용으로 비용이 증가되고, 처리 속도가 감소된다.
  <img src="https://velog.velcdn.com/images%2Fmardi2020%2Fpost%2F31ee5ff1-16be-457b-8dc7-8043b719c8f6%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-19%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.43.11.png"></img>

**2. Segmentation (세그멘테이션)**

- 사용자/프로그래머 관점의 메모리 기법
- 같은 크기의 페이지를 갖는 페이징 기법과 달리 **서로 다른 크기의 논리적 단위인 세그먼트로 분할한다.**
- 외부 단편화 존재 / 내부 단편화 해결
- CPU에서 해당 세그먼트의 크기를 넘어서는 주소가 들어오면 인터럽트가 발생해서 해당 프로세스를 강제로 종료
- 보호, 공유 측면에서 유리
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbm10Qc%2Fbtq8cNmxP8M%2FcjR6ViN20JuTWDBhaDrV90%2Fimg.png"></img>

---

### 내부 단편화

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FC8fcp%2FbtqZDP07SH0%2FIcPgUL9J9wtwcmvm7bZn40%2Fimg.png"></img>

- 프로세스를 메모리 빈 공간에 할당한 후 사용되지 않고 남아 있는 공간

### 외부 단편화

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FunngQ%2FbtqZOtBuQGg%2FI1pML2ksaoraHWpfp4JXHk%2Fimg.png"></img>

- 총 메모리 공간이 요청한 메모리 공간보다 크지만, 공간이 연속적이지 않아 발생하는 현상

---

## Reference

- https://jhnyang.tistory.com
- https://developyo.tistory.com/211?category=752792
- https://velog.io/@codemcd/운영체제OS-14.-세그멘테이션
- https://chelseashin.tistory.com/41
