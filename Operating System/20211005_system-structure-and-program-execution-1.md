> 반효경 교수님의 [운영체제](http://www.kocw.net/home/cview.do?cid=3646706b4347ef09) 강의를 듣고 정리하였습니다. 
>
> 또한, [infoqoch님의 블로그](https://velog.io/@infoqoch/%EC%BB%B4%ED%93%A8%ED%84%B0-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EA%B5%AC%EC%A1%B0)와  [HAEIN님의 블로그](https://jhi93.github.io/category/os/2019-11-25-operatingsystem-02-1/)를 참조하였습니다.




## 컴퓨터 시스템 구조

<img src="https://user-images.githubusercontent.com/71204049/135979335-81028e5f-430d-4f10-8530-b0d9718b6cb6.png" width="600"/>

(사진 출처: [KOCW](http://www.kocw.net/home/cview.do?cid=3646706b4347ef09))

### CPU

- CPU는 매 클럭마다 Memory에서 Instruction을 읽고 실행하는 것을 반복한다.

  - program counter는 다음으로 수행해야 할 instruction의 주소를 가리킨다.

  - CPU는 매번의 instruction마다 interrupt가 있는지 확인한다.

  - 만약 interrupt가 있으면 CPU의 사용 권한이 프로세스에서 운영체제(커널)로 넘어간다.

    

### Mode Bit

- 사용자가 프로그램의 잘못된 수행으로 다른 프로그램 및 운영체제에 피해가 가지 않도록 하기 위한 보호 장치 필요

- Mode Bit을 통해 하드웨어적으로 두 가지 모드의 operation 지원

  - ```
    - 1 사용자 모드: 사용자 프로그램 수행
    - 0 모니터 모드(= 커널 모드, 시스템 모드): OS 코드 수행
    ```

  - 보안을 해칠 수 있는 중요한 명령어는 모니터 모드에서만 수행 가능한 특권명령으로 규정

  - interrupt나 exception 발생 시 하드웨어가 mode bit을 0으로 바꿈

  - 사용자 프로그램에게 CPU를 넘기기 전에 mode bit을 1로 셋팅 

    <img src="https://user-images.githubusercontent.com/71204049/135985558-2459c329-159d-4667-b44b-670790e132d8.png" width="500"/>

    (사진 출처: [깃허브 블로그](https://jhi93.github.io/category/os/2019-11-25-operatingsystem-02-1/))

    

### 타이머(Timer)

- 특정 프로그램이 CPU를 독점하는 것으로부터 보호
- 정해진 시간이 흐른 뒤 운영체제에게 제어권이 넘어가도록 인터럽트를 발생시킴
- 타이머는 매 클럭 틱 때마다 1씩 감소
- 타이머 값이 0이 되면 타이머 인터럽트 발생
- time sharing을 구현하기 위해 널리 사용됨
- 현재 시간을 계산하기 위해서도 사용



### 시스템 콜(System Call)

- 시스템 콜이란, 사용자 프로그램이 운영체제의 서비스를 받기 위해 커널 함수를 호출하는 것



### 인터럽트(Interrupt)

- 현대 운영체제는 인터럽트에 의해 구동됨

- 인터럽트 당한 시점의 레지스터와 program counter를 save한 후 CPU의 제어를 인터럽트 처리 루틴에 넘긴다.
- interrupt(넓은 의미)
  - interrupt(하드웨어 인터럽트): 하드웨어가 발생시킨 인터럽트
    - timer: cpu의 독점 방지, 프로그램의 무한 루프에 대비하여 timer를 가진다.timer는 cpu를 일정 시간 이상 점유하면 cpu를 빼앗고 다음 프로세스에 cpu를 넘긴다.
    - I/O interrupt: I/O에서 입력이 발생하면 인터럽트가 되어 해당 값이 CPU로 이동한다.
    - DMA 컨트롤러의 인터럽트
  - Trap(소프트웨어 인터럽트):
    - Exception: 프로그램이 오류를 범한 경우
    - System Call: 프로그램이 커널 함수를 호출하는 경우
- 인터럽트 관련 용어
  - 인터럽트 벡터
    - 해당 인터럽트의 처리 루틴 주소를 가지고 있음
  - 인터럽트 처리 루틴(=Interrupt Service Routine, 인터럽트 핸들러)
    - 해당 인터럽트를 처리하는 커널 함수
  - 인터럽트가 발생하면 인터럽트 처리 루틴에 따라 cpu가 작동함(with 인터럽트 벡터)



### 입출력(I/O)의 수행

- 모든 입출력 명령은 특권 명령
- 사용자 프로그램은 어떻게 I/O를 하는가?
  - 시스템 콜(system call)
    - 사용자 프로그램은 운영체제에게 I/O 요청
  - trap을 사용하여 인터럽트 벡터의 특정 위치로 이동
  - 제어권이 인터럽트 벡터가 가리키는 인터럽트 서비스 루틴으로 이동
  - 올바른 I/O 요청인지 확인 후 I/O 수행
  - I/O 완료 시 제어권을 시스템콜 다음 명령으로 옮김



### Device Controller

- I/O device controller
  - 해당 I/O 장치 유형을 관리하는 일종의 작은 CPU
  - 제어 정보를 위해 control register, status register를 가짐
  - local buffer를 가짐(일종의 data register)
- I/O는 실제 device와 local buffer 사이에서 일어남
- Device controller는 I/O가 끝났을 경우 interrupt로 CPU에 그 사실을 알림



<u>device driver(장치구동기)</u> 

: OS 코드 중 각 장치별 처리루틴 -> software

<u>device controller(장치제어기)</u>

: 각 장치를 통제하는 일종의 작은 CPU -> hardware





