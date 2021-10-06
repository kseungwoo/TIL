> 반효경 교수님의 [운영체제](http://www.kocw.net/home/cview.do?cid=3646706b4347ef09) 강의를 듣고 정리하였습니다. 
>
> 또한, [infoqoch님의 블로그](https://velog.io/@infoqoch/%EC%BB%B4%ED%93%A8%ED%84%B0-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EA%B5%AC%EC%A1%B0)와  [HAEIN님의 블로그](https://jhi93.github.io/category/os/2019-11-26-operatingsystem-02-2/)를 참조하였습니다.




## 컴퓨터 시스템 구조

<img src="https://user-images.githubusercontent.com/71204049/135979335-81028e5f-430d-4f10-8530-b0d9718b6cb6.png" width="600"/>

(사진 출처: [KOCW](http://www.kocw.net/home/cview.do?cid=3646706b4347ef09))



### 동기식 입출력과 비동기식 입출력

<img src="https://user-images.githubusercontent.com/71204049/136191858-1ede8bb3-5d38-4898-9999-3d01c4c34863.png" width="600"/>

(사진 출처: [깃허브 블로그](https://jhi93.github.io/category/os/2019-11-26-operatingsystem-02-2/))

- 동기식 입출력 (synchronous I/O)
  - I/O 요청 후 입출력 작업이 완료된 후에야 제어가 사용자 프로그램에 넘어감
  - 입출력 작업이 완료되었음을 확인한 후 이어서 프로그램을 수행하고 싶을 때
  - 구현 방법 1
    - I/O가 끝날 때까지 CPU를 낭비시킴
    - 매 시점 하나의 I/O만 일어날 수 있음
  - 구현 방법 2
    - I/O가 완료될 때까지 해당 프로그램에게서 CPU를 빼앗음
    - I/O 처리를 기다리는 줄에 그 프로그램을 줄 세움
    - 다른 프로그램에게 CPU를 줌
- 비동기식 입출력 (asynchronous I/O)
  - I/O가 시작된 후 입출력 작업이 끝나기를 기다리지 않고 제어가 사용자 프로그램에 즉시 넘어감
  - 입출력 작업의 완료와 상관 없이 이어서 프로그램을 수행하고 싶을 때



** 두 경우 모두 I/O의 완료는 인터럽트로 알려줌



### DMA (Direct Memory Access)

<img src="https://user-images.githubusercontent.com/71204049/136193934-e46700da-8235-4307-bff2-a6930bfa93ce.png" width="900"/>

(사진 출처: [Quora](https://www.quora.com/What-is-the-function-of-DMA-in-a-computer))

- 빠른 입출력 장치를 메모리에 가까운 속도로 처리하기 위해 사용
- CPU의 개입 없이 I/O 장치와 메모리 사이의 데이터를 전송하는 접근 방식 
  - CPU의 중재 없이 device controller가 device의 buffer storage의 내용을 메모리에 block 단위로 직접 전송
- 바이트 단위가 아니라 block 단위로 인터럽트를 발생시킴
  - 고속의 I/O 장치의 경우 빈번한 인터럽트가 발생하는데 DMA를 사용함으로써 프로그램 수행 중 인터럽트 발생 횟수를 최소화한다.
- 메모리에 접근할 수 있는 장치는 원래 CPU밖에 없음



### 서로 다른 입출력 명령어

- I/O를 수행하는 special instruction에 의해(isolated I/O)
- Memory Mapped I/O에 의해

<img src="https://user-images.githubusercontent.com/71204049/136195091-a10e1806-7ea0-4019-b7d2-77028692a878.png" width="600"/>

(사진 출처: [티스토리](https://tkdguq0110.tistory.com/entry/Memory-Mapped-IO))



### 저장장치 계층구조

<img src="https://user-images.githubusercontent.com/71204049/136195949-e95e25d5-89d6-49b6-9980-b3f0e5004ce0.png" width="600"/>

(사진 출처: [깃허브 블로그](https://imbf.github.io/computer-science(cs)/2020/08/21/What-is-The-Operating-System.html))

- Primary(Executable)은 CPU가 직접 접근 가능함 (Byte 단위의 접근이 가능)
- Secondary는 CPU가 직접 접근하지 못 (Sector 단위의 접근이 가능)
- Cache는 register와 main memory 간의 속도 차를 완충하기 위해서 존재 (컴퓨터의 성능을 향상시키기 위해 사용)
  - CPU와 주기억장치 사이에 존재, 자주 사용되는 데이터를 기억
  - 데이터의 재사용
    - 상대적으로 느린 메인 메모리 접근 횟수를 줄임



### 프로그램의 실행 (메모리 load)

<img src="https://user-images.githubusercontent.com/71204049/136197341-73d32d7f-b401-4114-b97a-f2cc73066461.png" width="600"/>

(사진 출처: [깃허브 블로그](https://imbf.github.io/computer-science(cs)/2020/08/21/What-is-The-Operating-System.html))

- 프로그램들은 처음에 실행파일 하드디스크에 저장

  - 실행파일을 실행하면 메모리에 로드되고 이것이 프로세스

- 정확히는 물리적 메모리(Physical Memory)에 바로 올라가지 않고 가상 메모리(Virtual Memory)를 거친다.

  - 프로그램 실행 시 Address Space(각 프로그램마다 독자적으로 가지고 있는 가상 메모리 주소 공간)가 만들어짐. 종료 시 사라짐

    - ```
      Stack: 함수 호출 및 리턴
      Data: 지역 변수, 전역 변수, 자료구조
      Code: 프로그램 기계어 코드
      ```

    - 메모리를 낭비하지 않기 위해, 당장 필요한 것만 물리적 메모리에 존재

    - 나머지 부분은 프로그램 종료시까지 Swap Area에 존재

- kernel은 컴퓨터 부팅 이후 항상 메모리에 상주

- Swap Area
  - 메모리 용량의 한계로, 메모리 연장 공간으로써 사용



### 커널 주소 공간의 내용

<img src="https://user-images.githubusercontent.com/71204049/136199202-986abff2-88a3-4d99-ba7d-3a166e8f86b1.png" width="750"/>

(사진 출처: [깃허브 블로그](https://imbf.github.io/computer-science(cs)/2020/08/21/What-is-The-Operating-System.html))



### 사용자 프로그램이 사용하는 함수

- 사용자 정의 함수
  - 자신의 프로그램에서 정의한 함수
- 라이브러리 함수
  - 자신의 프로그램에서 정의하지 않고 갖다 쓴 함수
  - 자신의 프로그램의 실행 파일에 포함되어 있다.
- 커널 함수
  - 운영체제 프로그램의 함수
  - 커널 함수의 호출 = 시스템 콜
- 사용자 정의 함수와 라이브러리 함수는 해당 프로세스의 address space 공간 code 영역에 존재
- 커널 함수는 커널의 address space 공간 code 영역에 존재



### 프로그램의 실행

<img src="https://user-images.githubusercontent.com/71204049/136200922-c6de3712-f6e7-4f39-ab20-2e816e7d8427.png" width="850"/>

(사진 출처: [벨로그](https://velog.io/@gojaegaebal/210207-%EA%B0%9C%EB%B0%9C%EC%9D%BC%EC%A7%8062%EC%9D%BC%EC%B0%A8-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9COS-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-2-0-User-mode-Kernel-mode))
