# Process

[TOC]

## 프로세스의 개념

![프로세스의 개념](C:\Users\multicampus\Desktop\CS-Study\이덕배\운영체제\02. Process\assets\프로세스의 개념.png)

> 프로세스 = 실행 중인 프로그램
>
> 프로세스의 현재 상태를 정확하게 이해하려면 프로세스 문맥, 즉 프로세스의 탄생부터 종료까지 무엇을, 어떻게 실행했는지를 알아야 한다.



#### 프로세스의 상태

![프로세스 상태도](C:\Users\multicampus\Desktop\CS-Study\이덕배\운영체제\02. Process\assets\프로세스 상태도.png)

> CPU는 매 순간 하나의 프로세스만을 잡고 있는다.

- Running: CPU를 잡고 instruction을 수행중인 상태
- Ready: CPU를 기다리는 상태(메모리 등 다른 조건을 모두 만족해야 함)
- Blocked(wait, sleep)
  - CPU를 주어도 당장 instruction을 수행할 수 없는 상태
  - Process 자신이 요청한 event(cf. I/O)가 즉시 만족되지 않아 이를 기다리는 상태

<hr>

- New: 프로세스가 생성중인 상태
- Terminated: 수행(execution)이 끝난 상태

![프로세스의 상태](C:\Users\multicampus\Desktop\CS-Study\이덕배\운영체제\02. Process\assets\프로세스의 상태 (2).png)

- CPU는 빠르게 그리고 공유하는 자원이기 때문에 프로세스가 돌아가며 사용함



#### PCB

![pcb](C:\Users\multicampus\Desktop\CS-Study\이덕배\운영체제\02. Process\assets\pcb.png)

> 운영체제가 각 프로세스를 관리하기 위해 프로세스당 유지하는 정보

- OS가 관리상 사용하는 정보
- CPU 수행 관련 하드웨어 값
- 메모리 관련
- 파일 관련
