> 반효경 교수님의 [운영체제](http://www.kocw.net/home/cview.do?cid=3646706b4347ef09) 강의를 듣고 정리하였습니다. 
>



## CPU burst vs I/O burst

- 프로세스는 CPU burst와 I/O burst를 전환하며 프로그램을 실행
- CPU burst
  - CPU 명령을 실행하는 것
- I/O burst
  - I/O를 요청한 다음 기다리는 시간
- CPU bound process
  - CPU burst가 큰 프로세스
  -  few very long CPU bursts
- I/O bound process
  - I/O burst가 큰 프로세스
  -  many short CPU bursts



## CPU 스케줄링

- CPU를 얻고자하는 프로세스들 중에서 어떠한 프로세스에게 CPU를 줄 것인지 결정하는 것
- 여러 종류의 job(=process)이 섞여 있기 때문에 CPU 스케줄링이 필요하다.
- Interactive Job에게 적절한 response 제공 요망
- CPU와 I/O 장치 등 시스템 자원을 골고루 효율적으로 사용



## 스케줄링 성능 척도

- CPU Utilization (이용률)
  - keep the CPU as busy as possible
- Throughput (처리량)
  - number of processes that complete their execution per time unit
- Turnaround Time (소요시간, 반환시간)
  - amount of time to execute a particular process (in ready queue)
  - 특정 작업이 완료될 때까지 걸린 시간 
- Waiting time (대기 시간)
  - amount of time a process has been waiting in the ready queue
  - 특정작업을 CPU가 실행하지 않은 시간들을 합한 시간
- Response time (응답 시간)
  - amount of time it takes from when a request was submitted until the first response is produced, not output (for time-sharing environment)
  - 특정 작업이 처음 실행되기까지 걸린 시간



## FCFS (First-Come First-Served)

- 먼저 온 순서대로 처리
- 비선점형 스케줄링
- 앞선 프로세스의 시간이 길어지면 전체 시스템의 평균 대기시간이 길어진다는 단점
- Convoy Effect(호위효과) 발생
  - 앞선 프로세스가 실행시간이 길어 실행시간이 짧은 프로세스들이 실행되지 못하고 지나치게 오래 기다리는 상황



## SJF (Shortest Job First)

- 각 프로세스의 다음번 CPU burst time을 가지고 스케줄링에 활용
- CPU burst time이 가장 짧은 프로세스를 제일 먼저 스케줄
- Two schemes
  - Nonpreemptive
    - 일단 CPU를 잡으면 이번 CPU burst가 완료될 때까지 CPU를 선점(preemption) 당하지 않음
  - Preemptive
    - 현재 수행중인 프로세스의 남은 burst time보다 더 짧은 CPU burst time을 가지는 새로운 프로세스가 도착하면 CPU를 빼앗김
    - 이 방법을 Shortest-Remaining-Time-First(SRTF)이라고도 부른다
- SJF is optimal
  - 주어진 프로세스들에 대해 minimum average waiting time을 보장
- 두 가지 문제점
  - Starvation(기아 현상)
    - CPU burst time이 긴 작업은 영원히 실행되지 못할 수도 있음
  - 다음 CPU burst time의 예측할 수 있는가?
    - 정확한 예측은 불가
    - 추정(estimation)만이 가능하다.
      - 과거의 CPU burst time을 이용해서 추정



## Priority Scheduling (우선순위 스케줄링)

- 우선순위가 제일 높은 프로세스에게 CPU를 주겠다.
- Both Preemptive and Nonpreemptive Possible
- SJF는 일종의 priority shceduling이다.
  - priority = predicted next CPU burst time
- Problem
  - Starvation(기아 현상): 낮은 우선순위의 프로세스들은 영영 실행되지 못할 수 있다.
- Solution
  - Aging(노화): 시간이 지날수록 프로세스의 우선순위를 증가시키는 방식



## Round Robin (RR)

- 각 프로세스는 동일한 크기의 할당 시간(time quantum)을 가짐 (일반적으로 10-100 ms)
- 할당 시간이 지나면 프로세스는 선점(preempted)당하고 ready queue의 제일 뒤에 가서 다시 줄을 선다
- n개의 프로세스가 ready queue에 있고 할당 시간이 q time unit인 경우 각 프로세스는 최대 q time unit 단위로 CPU 시간의 1/n을 얻는다.
  - 어떤 프로세스도 (n-1)q time unit 이상 기다리지 않는다.
- Performance
  - q large -> FIFO
  - q small -> Context Switch 오버헤드가 커진다.
- 일반적으로 SJF보다 avrage turnaround time이 길지만 response time은 더 짧다.
