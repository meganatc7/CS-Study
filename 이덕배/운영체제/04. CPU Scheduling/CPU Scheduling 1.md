# CPU Scheduling 1

[TOC]

## 📑 CPU Scheduling 개념 및 지난 시간 복습

![bursts](assets/bursts.png)

- CPU Scheduling

  > ready queue에 들어와 있는 CPU를 얻기 위해 대기 중인 프로세스들 중에 어떤 프로세스에게 cpu를 줄지 결정하는 것

- CPU Scheduling의 2가지 이슈

  - 누구한테 CPU를 줄 것인가

  - 실행 중인 프로세스를 끝까지 기다릴 것인가 혹은 중간에 CPU를 뺏을 것인가

    (cf. 끝까지 기다린다면 긴 프로세스가 들어왔을 때 대기 시간이 증가할 수 있음)

- ==preemptive== : CPU의 자진 반납을 기다리는 방법(비선점형)

- ==nonpreemptive== : 강제로 CPU 빼앗을 수 있는 방법(선점형)



#### CPU 스케줄링을 위한 성능 척도

<img src="assets/척도.png" alt="성능 척도" style="zoom:150%;" />

- 분류

  - ==시스템 입장==에서의 성능 척도

    > 시스템 입장에서는 최대한 일을 많이 시키는 것이 좋음

    - 이용률 : CPU가 놀지 않고 일한 시간의 비율
    - 처리량 : 주어진 시간동안 완수한 작업의 수

  - ==프로그램 입장==에서의 성능 척도

    > 고객 입장으로 CPU를 빨리 얻어 빨리 작업을 수행하면 좋음

    - turnaround time(소요 시간, 반환 시간) : CPU를 쓰기 위해 대기하로 들어와 다 쓰고 나갈 때까지 걸린 시간(cpu burst가 종료될 때까지의 시간)

      cf. 기다렸다가 + running, 즉 프로세스가 시작~종료까지의 시간이 아닌 대기~ 종료(ex. I/O작업) 위해 나갈 때까지의 시간

    - waiting time(대기 시간) : 순수하게 대기한 시간

    - responsse time(응답 시간) : ready queue에 들어와 처음으로 CPU를 얻기까지의 시간

      cf. 처음으로 CPU를 얻기까지의 시간은 사용자 경험에 중요

    cf. waiting time vs. response time : 선점형 스케줄링의 경우 CPU를 한 번 얻었다고 끝까지 쓰는 것이 아님 -> waiting time이 여러 차례 발생 가능 / response time은 최조의 CPU의 시간을 얻기까지의 시간만 의미



#### CPU Scheduling Algorithms

<img src="assets/알고리즘.png" alt="CPU Scheduling Algorithms" style="zoom:150%;" />

##### FCFS

> First-Come First-Served

<img src="assets/fcfs.png" alt="CPU Scheduling Algorithms" style="zoom:150%;" />

- 오는 순서대로 처리
- ==비선점형==
- 썩 효율적이지는 않음 => 오래 걸리는 프로세스가 CPU를 선점할 경우 비효율적
- 앞에 어떤 프로세스가 있는가가 기다리는 시간(대기 시간)에 상당한 영향을 미침

<img src="assets/fcfs(2).png" alt="CPU Scheduling Algorithms" style="zoom:150%;" />

- ==Convoy effect== : 긴 프로세스의 선점으로 인해 짧은 프로세스들이 기다리는 현상



##### SJF

> Shortest-Job-First

<img src="assets/sjf.png" alt="CPU Scheduling Algorithms" style="zoom:150%;" />

- CPU를 사용하고자 하는 시간, 즉 cpu burst가 가장 짧은 프로세스에게 CPU를 주는 방식

- 효율성 up

- average waiting time 최소화 가능(preemptive의 경우)

- preemptive 방식(더 짧은 프로세스가 등장하면 그 프로세스에게 cpu를 넘겨줌 => shortest remaing time) / nonpreemtive 방식 모두 사용 가능

  - nonpreemtive :  cpu 스케줄링이 이루어지는 시점 == ==cpu를 다 쓰고 나가는 시점==

    <img src="assets/sjf(2).png" alt="CPU Scheduling Algorithms" style="zoom:150%;" />

    |      | 처리 순서 | 대기 시간       |
    | ---- | --------- | --------------- |
    | P1   | 1번 처리  | 0초             |
    | P2   | 3번 처리  | (7+1-2) = 6초   |
    | P3   | 2번 처리  | (7-4) = 3초     |
    | P4   | 4번 처리  | (7+1+4-5) = 7초 |

  - preemptive : cpu 스케줄링이 이루어지는 시점 == ==새로운 프로세스가 도착하는 시점==

    <img src="assets/sjf(3).png" alt="CPU Scheduling Algorithms" style="zoom:150%;" />

    |      | 처리 순서 | 사용 시간   | 대기 시간                            | 남은 시간     |
    | ---- | --------- | ----------- | ------------------------------------ | ------------- |
    | P1   | 1 / 6     | 2(1)        | 0(1) + 2(2) + 1(3) + 2(4) + 4(5) = 9 | 5(1~5), 0(6)  |
    | P2   | 2 / 4     | 2(2) / 2(4) | 0(2) + 1(3) = 1                      | 2(2, 3), 0(4) |
    | P3   | 3         | 1(3)        | 0(3)                                 | 0(3)          |
    | P4   | 5         | 4(5)        | 2(5)                                 | 0(5)          |

- 2가지 문제점

  - starvation(기아 현상) : CPU 사용 시간이 긴 프로세스는 CPU 할당을 받기까지 오랜 시간 기다려야 함

    <img src="assets/problem.png" alt="CPU Scheduling Algorithms" style="zoom:150%;" />

  - 실제로 프로세스들은 자신의 CPU 사용 시간을 알기 어려음(->과거 사용 기록을 통해 추정)

    <img src="assets/예측.png" alt="CPU Scheduling Algorithms" style="zoom:150%;" />

    - t : 실제 CPU 사용 시간 / 타우(τ) : CPU 예측 사용 시간

      <hr>
  <img src="assets/공식.png" alt="공식" style="zoom:150%;" />
  
- 계산 결과 => 현재를 기준으로 최근의 가중치를 높게 반영하여 계산



##### Priority Scheduling

> 우선 순위 스케줄링(우선 순위가 높은 프로세스에게 CPU 할당)

![우선순위](assets/우선순위.png)

- preemptive(더 높은 우선 순위의 프로세스 등장 시 CPU 재할당) / nonpreemptive(현재 실행 중인 프로세스에게 CPU보장) 방법 둘 다 가능
- 리눅스와 같은 대부분의 운영체제에서 작은 숫자일 수록 높은 우선 순위를 지님
- FJS 역시 우선 순위 스케줄링의 일종(CPU 사용 시간으로 우선 순위 결정)
- Starving 발생 가능 => Aging(노화) 사용: 우선 순위가 낮은 프로세스라도 오랜 시간 기다렸다면 우선 순위를 높여줌



##### Round Robin(RR)

![Round Robin](assets/rr.png)

- 현대적인 컴퓨터 시스템은 RR에 기반

- CPU를 줄 때 할당 시간을 세팅해서 주고, 할당 시간을 넘기면 time interrupt를 발생시켜 CPU를 재할당 시키는 것도 RR 스케줄링에 기반(선점형)

- ==응답 시간(Response time)==을 빠르게 만들어줌(조금씩 시간을 줬다 뺐었다)

- CPU 사용 시간이 긴 프로세스는 긴 대기 시간을, 짧은 프로그램은 짧은 대기시간을 가짐

  ==대기 시간이 본인의 CPU 사용 시간에 비례==

- 극단적인 예시

  - 할당 시간이 매우 큰 경우 : ==FCFS==와 같은 역할
  - 할당 시간이 매우 작은 경우 : 빈번한 ==context switch 발생 -> overhead 발생==

- ![Round Robin](assets/ex.rr.png)

  - RR은 SJF보다 ==average turnaround time/대기 시간은 길지만 응답 시간은 더 짧음==

  - CPU 사용 시간이 무분별하거나 모를 경우 사용하기 좋은 방법

    CPU 사용 시간이 모두 동이할 경우 좋지 않음(거의 동시에 모든 프로세스 종료 => 하나씩 실행시키면 순차적으로 빠르게 종료)

- ![Round Robin](assets/ex.rr(2).png)

  - cf. 위는 헤테로 지니어스들로 이루어진 문제로 RR에 호의적인 예제는 아니다
