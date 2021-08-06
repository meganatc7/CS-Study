# process synchronization 2

[toc]

## Semaphores

### meaning of Semaphore

![Semaphores](assets\02\semaphores.png)

- semaphore
  - 멀티프로그래밍 환경에서 공유 자원에 대한 접근을 제한하는 방법
  - 일종의 추상 자료형으로 object와 operation으로 구성(실제 프로세스가 어떤게 구현되는가와는 별개의 자료형)
  - semaphore의 변수 S(정수형)  : 자원의 개수를 의미
  - P(s) : 세마포어 변수 값을 획득하는 로직(공유 자원을 획득)
  - V(s) : 세마포어 변수 값을 반환하는 로직(획득했던 공유 자원을 반납)
  - P와 V는 atomic하게 일어난 다는 것을 가정
  - semaphore을 사용해도 busy waiting 문제 발생(while문을 돌다가 본인에게 할당된 CPU 시간을 다 쓸 수 있음)



### Critical Section of n Processes

![crtical section of n processes](assets\02\crticalsection.png)

- critical section에서 semaphore를 사용하면 critical section 문제 해결 가능
- 프로그래머는 semaphore가 지원되면 P, V에 대한 연산만 진행(P, V의 구현은 시스템에서 그때그때 진행) 
- busy wait(=spin lock) 발생 가능



### Block / Wake

![block/wake](assets\02\blockwake.png)

- busy wait를 방지할 수 있음
- semaphore의 변수값(S)와 세마포어로 인해 잠들어있는 프로세스를 연결하 위한 Queue(L)
- semaphore를 기다리면서 잠드는 프로세스를 연결



![block/wake](assets\02\blockwake(2).png)

- P 자원 획득 과정
  - 여분이 있는 경우에는 바로 획득
  - 여분이 없는 경우에는 잠에 들며 L(잠든 리스트)에 추가됨
- V 자원 반납 과정
  - 자원 반납과 잠든 프로세스의 존재 유무를 확인하고 잠든 프로세스가 있을 경우 wakeup시켜줌
- 기준점 확인하기(0이하/0미만)
- S가 음수일 경우 -> 잠든 프로세스가 있다 / 양수일 경우 -> 여분이 있다.



### Busy wait vs. Block/wakeup

![better](assets\02\better.png)

- 일반적으로 Block/wakeup이 효율적 -> CPU의 의미있는 이용률을 높일 수 있음

- 굳이 단점을 꼽자면, Block/wakeup의 경우 overhead 발생 가능(상태 변화가 일어나며 발생)

  -> 길이가 매우 짧을 경우 busy-wait가 나을 수 있음



### Two types of Semaphores

![types](assets\02\types.png)

- Binary semaphore: 자원의 개수가 하나일 경우(mutual exclusion에 주로 사용)
- Counting semaphore: semaphore 변수가 0 or 1이 아닌 경우로 자원이 여러 개 있는 경우를 의미(여분의 자원 카운팅)



### Deadlock and Starvation

![dealock](assets\02\deadlock.png)

- Deadlock: 서로 자신의 것을 놓지 않고 상대방을 기다리며 영원한 기다림이 발생하는 경우

- 순서를 지정해주면 자연스럽게 문제를 해결할 수 있음(ex. 자원 Q는 S를 끝낸 후 얻을 수 있음)

- starvation 발생 가능 : 특정 친구가 무한히 기다려야 하는 경우 발생 가능

  ![dining example](assets\02\dining.png)

  

