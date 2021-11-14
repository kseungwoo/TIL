> 반효경 교수님의 [운영체제](http://www.kocw.net/home/cview.do?cid=3646706b4347ef09) 강의를 듣고 정리하였습니다. 
>



## Multi-Level Queue

- Ready queue를 여러 개로 분할
  - foreground(interactive)
  - background(batch - no human interaction)
- 각 큐는 독립적인 스케줄링 알고리즘을 가짐
  - foreground -RR
  - background - FCFS
- 큐에 대한 스케줄링이 필요
  - Fixed priority shceduling
    - serve all from foreground then from background
    - Possibility of starvation
  - Time slice
    - 각 큐에 CPU time을 적절한 비율로 할당
    - Eg. 80% to foreground in RR, 20% to backgroun in FCFS.



## Multi-Level Feedback Queue

- 프로세스가 다른 큐로 이동 가능
- 에이징(aging)을 이와 같은 방식으로 구현할 수 있다.
- Multi Level Feedback Queue Scheduler를 정의하는 파라미터들
  - Queue의 수
  - 각 큐의 scheduling algorithm
  - process를 상위 큐로 보내는 기준
  - process를 하위 큐로 보내는 기준
  - 프로세스가 CPU 서비스를 받으려 할 때 들어간 큐를 결정하는 기준

- 예시
  - 3개의 큐
    - Q0 - time quantum 8ms
    - Q1 - time quantum 16ms
    - Q2 - FCFS
  - 스케줄링
    - new job이 queue Q0로 들어감
    - CPU를 잡아서 할당시간 8ms동안 수행됨
    - 8ms 동안 다 끝내지 못했으면 queue Q1으로 내려감
    - Q1에 줄서서 기다렸다가 CPU를 잡아서 16ms 동안 수행됨
    - 16ms에 끝내지 못한 경우 queue Q2로 쫓겨남



## Multiple-Processor Scheduling

- CPU가 여러 개인 경우 스케줄링은 더욱 복잡해짐
- Homogeneous processor인 경우
  - Queue에 한 줄로 세워서 각 프로세서가 알아서 꺼내가게 할 수 있다.
  - 반드시 특정 프로세서에게 수행되어야 하는 프로세스가 있는 경우에는 문제가 더 복잡해짐
- Load sharing
  - 일부 프로세서에 job이 몰리지 않도록 부하를 적절히 공유하는 메커니즘 필요
  - 별개의 큐를 두는 방법 vs. 공동 큐를 사용하는 방법
- Symmetric Multiprocessing (SMP)
  - 모든 프로세서가 대등
  - 각 프로세서가 각자 알아서 스케줄링 결정
- Asymmetric Multiprocessing
  - 하나의 프로세서가 시스템 데이터의 접근과 공유를 책임지고 나머지 프로세서는 거기에 따름



## Real-Time Scheduling

- Hard real-time systems
  - Hard real-time task는 정해진 시간 안에 반드시 끝내도록 스케줄링해야 함
- Soft real-time computing
  - Soft real-time task는 일반 프로세스에 비해 높은 priority를 갖도록 해야 함



## Thread Scheduling

- Local Scheduling
  - User level thread의 경우 사용자 수준의 thread library에 의해 어떤 thread를 스케줄할지 결정
  - 사용자 프로세스가 직접 스레드를 관리하고 운영체제는 그 스레드의 존재를 모른다.

- Global Scheduling
  - Kernel level thread의 경우 일반 프로세스와 마찬 가지로 커널의 단기 스케줄러가 어떤 thread를 스케줄할지 결정
  - 운영체제가 스레드의 존재를 알고 있는 상황



## Algorithm Evaluation

- Queueing Models
  - 확률 분포로 주어지는 arrival rate와 service rate 등을 통해 각종 performance index 값을 계산
- Implementation(구현) & Measurement(성능 측정)
  - 실제 시스템에 알고리즘을 구현하여 실제 작업(workload)에 대해서 성능을 측정 비교
- Simulation (모의 실험)
  - 알고리즘을 모의 프로그램으로 작성 후 trace를 입력으로 하여 결과 비교
