# CPU Scheduling 2

[toc]

### 지난 시간 리뷰

#### 컴퓨터 스케줄링의 필요성

- 컴퓨터 시스템 안의 job들은 호모 지니어스 하지 않고, I/O bound와 CPU bound job이 섞여있기 때문



#### Scheduling Algorithm

![algo](assets\algo.png)

##### FCFS 

- 오래 걸리는 CPU 선점할 경우 대화형 프로세스(I/O bound job)가 오래 기다려야 함



##### RR 

- heterogeneous job들에게 효율적이며 공평함(할당된 시간을 번갈아가며 사용 -> 대기 시간이 프로세스가 cpu를 사용해야하는 시간과 비례)

- cf. RR은 프로세가 CPU를 빼앗길 때 context를 저장하고 다시 얻는 시점에 저장된 지점부터 재개할 수 있는 매커니즘 덕분에 가능



##### Multilevel Queue

- ready queue를 여러 줄로 분할

![multilevel](assets\multilevel(2).png)

- 위에 있을 수록 우선순위가 높음(계급제)

- 태어난 계급(순위)에 따라 결정되며 우선 순위를 극복할 수 없음

- issue

  - 프로세스를 어떤 줄에 할당할 것인가?

  - 우선 순위가 높은 줄이 비어있지 않다면 무조건적으로 높은 계급에게만 CPU를 할당할 것인가?(starvation 발생 가능)

  - ![multilevel](assets\multilevel.png)

    - ready queue를 여러 개로 분할

      - foreground : RR
      - background : FCFP(context switch overhead 줄이기)

      => queue에 대한 스케줄링 필요

      - fixed priority scheduling : 무조건 우선 순위에 따라 할당
      - Time slice : starvation 방지 (ex. 80%는 우선 순위가 높은 큐 / 20%는 낮은 큐에 cpu 할당)

- 공정하지 않고 차별적인 방법

- 우선순위가 중요하지만 이와 같은 방식은 신분 변경 불가능

  => Multilevel Feedback Queue 등장



#####  Multilevel Feedback Queue

![multilevel](assets\multilevel(5).png)

![multilevel](assets\multilevel(4).png)

- Multilevel Queu와 마찬가지로 ready queue가 여러 줄로 분할되지만, 출신 변경이 가능

- issue

  - queue를 몇개를 둘 것인가
  - 각 큐에 대한 스케줄링은 어떻게 할 것인가
  - 우선순위 변동의 기준으로 무엇으로 할 것인가
  - 처음 프로세스가 들어올 때 어느 큐로 들어갈 것인가

  cf. 주로 처음 들어오는 프로세스의 경우 우선 순위가 가장 높은 큐에 넣음.

  ​	우선 순위가 높을 수록 quantum을 짧게 주고, 우선 순위가 가장 낮은 큐는 FCFS 방식 사용

  ​	CPU burst가 짧은 프로세스는 바로 끝낼 수 있고, 반대의 경우 시간은 점점 더 받게 되지만, 우선순위가 떨어지게 된다.

- CPU 사용 시간이 짧은 프로세스에게 우선 순위 부여

- 프로세스들의 CPU 사용 시간에 대한 예측이 불필요



<hr>

지금까지는 CPU가 하나 뿐인 시스템의 경우, 아래는 CPU가 여러 개 있거나 혹은 deadline/thread가 있는 등의 상황에서의 스케줄링



##### Multi-Processor Scheduling(CPU가 여러개 있는 경우)

![Multi-Processor](assets\multiple.png)

- Homogenous processor : 한 줄로 세워 처리
  - 특정 job이 특정 CPU에서 수행되어야 할 경우에는 주로 먼저 할당한 다음 스케줄링 진행
- Load sharing
  - 한 줄 서기 vs. 각각의 CPU마다 줄 서게 하기
- Symmetric Multiprocessing
  - 모든 CPU들이 대등
- Asymmetric multiprocessing
  - 하나의 CPU가 전체적인 컨트롤 담당(데이터 접근과 공유를 책임지고 나머지는 거기에 따름)



##### Real-Time Scheduling

![real-time](assets\real-time.png)

- real time job : deadline이 정해져있는 잡(정해진 시간 내에 반드시 실행되어야 함)
- CPU 스케줄링 시 데드라인 보장 Need
- real-time scheduling은 그때 그때 스케줄링하기보다는 미리 스케줄링을 하여 데드라인이 보장되도록 적재적소에 배치
- cf. 이런 경우는 주기적인 성격을 가진 job이 많음
- Hard real-time systems : 반드시 데드라인이 보장되어야 함
- Soft real-time scheduling : 데드라인을 지켜야 하지만, 그 강도가 hard 리얼 타임 잡보다 강하지 않음



##### Tread Sceduling

![thread](assets\thread.png)

- cf. 스레드: 프로세스 하나에 여러 개의 CPU 수행 단위가 있는 것
- Local Scheduling
  - 유저 레벨 스레드(운영 체제가 스레드의 존재를 모름, 사용자가 직접 관리)에서 운영체제는 프로세스에게 CPU를 줄 지 말지만 결정하고, 그 프로세스에 CPU가 갔을 때 어떤 thread에게  CPU를 줄 지는 로컬에서 결정(os가 아니라 사용자 프로세스가 직접 결정)
- Global Scheduling
  - 커널 스레드(운영 체제가 스레드의 존재를 알고 있음)에서 운영 체제가 프로세스 스케줄링 하듯 어떤 스레드에게 CPU를 줄지 결정