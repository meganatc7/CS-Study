# System Structure & Program Execution 1

> 운영체제 공부에 앞서 하드웨어와 프로그램의 구동 방식에 대한 학습 진행

[TOC]

## 컴퓨터 시스템의 구조

![컴퓨터시스템구조](assets\컴퓨터시스템구조.png)

- input과 output으로 구성
- Memory는 CPU의 작업 공간
- I/O 디바이스는 별개의 구조로 생각하면 됨
- (하드)디스크: 보조 기억 장치이자 I/O 디바이스로도 사용 가능한 장치



#### CPU & Memory

> 메모리는 CPU의 작업공간

- CPU는 매클럭, 메모리에 있는 명령들을 실행

- register: 메모리보다 빠르고 정보를 저장할 수 있는 저장공간

- I/O 디바이스에 직접 접근 X

- CPU에서 디스크 접근 필요시  device 컨트롤러에게 요청(디바이스는 디스크에서 정보를 가져와 local buffer에 저장, CPU는 다른 작업 진행 ---> 사용자가 Interactive하게 느낌)

- 메모리에 있는 사용자 프로그램이 I/O 작업이 필요할 때는 CPU를 OS한테 넘겨주고 OS가 처리하도록 진행 (보안 목적)

  

#### timer

> for문, while문과 같은 이유로 무한루프에 빠지게 되면 CPU가 하나의 프로그램에 갇힐 수 있다.
>
> 타이머는 제한 시간을 설정해 특정 프로그램이 CPU를 독점하는 것을 방지하여 위와 같은 현상을 막는다.

- CPU 작업 중 세팅 시간 오버시 타이머가 Interrupt를 보내 CPU의 제어권을 프로그램에서 운영체제로 이동하게 만든다. 운영체제는 타이머를 재설정하고 다음 프로그램에게 CPU를 보내주는 작업을 반복한다.
- time sharing 목적



#### mode bit

> CPU 제어권을 가지고 있는 주체를 구분하기 위한 장치

- Mode bit == 1: 사용자 모드(사용자 프로그램 수행)

  제한된 instruction만 실행 가능(보안 목적) 

- Mode bit == 0: 모니터 모드(OS 코드 수행)

  모든 instruction 실행 가능(특권명령 수행 가능)



#### device controller

- I/O 디바이스 컨트롤러
  - 해당 I/O 장치유형을 관리하는 일종의 작은 CPU
  - control register, status register for 제어정보
  - ocal buffer: 실제 데이터 저장 위치(일종의 data register)
- I/O는 실제 device와 local buffer사이에서 발생



#### DMA controller

> 메모리에 직접 접근할 수 있는 컨트롤러
>
> I/O장치가 자주 interrupt 발생 시 CPU에 방해가 될 수 있음. 그래서 DMA controller를 통해 CPU는 메모리에 있는 자신의 일을 진행하게 만들어 주고, DMA controller는 중간중간 들어오는 값들을 메모리로 복사해 한 번에 전달

- memory controller: 메모리에 대한 CPU와 DMA의 동시 접근 방지 역할



#### * System call

> 운영체제에게 부탁하는 것
>
> 트랩을 이용해 인터럽트를 걸어서 실행

- CPU가 순차적으로 실행되지 않고 instruction의 메모리 주소 이동 && 프로그램이 직접 인터럽트 라인을 만드는 instruction 실행

- CPU는 인터럽트를 받으면 OS로 CPU 운영권 이동
- 운영체제는 device controller(해당 I/IO 장치를 관리하는 일종의 작은 CPU)에게 부탁하고interrupt가 끝날 시 CPU에게 전달



#### Interrupt

- 인터럽트 당한 시점의 레지스터와 program counter를 save한 후 CPU 제어를 인터럽트 처리 루틴에 넘김

- 넓은 의미의 Interrupt

  - Interrupt(하드웨어 인터럽트)

    > 하드웨어가 발생시킨 인터럽트(요청 작업 완료 소식 전달, I/O controller가 전달)

  - Trap(소프트웨어 인터럽트)

    > I/O 요청을 위한 시스템 콜

    - Exception: 프로그램이 오류를 범한 경우
    - System call: 프로그램이 커널 함수를 호출하는 경우
