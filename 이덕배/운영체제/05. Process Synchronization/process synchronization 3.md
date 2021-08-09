# process synchronization 3

[toc]

## Classical Problems of Synchronization

> Synchronization의 3가지 문제점

![problem](assets\03\problem.png)



### Bounded-Buffer Problem(Producer-Consumer Problem)

![bb](assets\03\bb.png)

- 생산자-소비자 문제(producer-consumer problem)
  - 생산자: 공유 버퍼에 데이터를 만들어 넣는 역할(여러개)
  - 소비자: 생산자가 만든 데이터를 사용하는 역할(여러개)
- Buffer: 임시로 데이터를 저장하는 공간 => Buffer의 크기가 유한해 문제가 발생
  - 생산자 입장에서 - 동시에 데이터를 만들어 넣을 때
  - 소비자 입장에서 - 동시에 같이 데이터에 접근할 경우
  - 버퍼가 다 찬 상태(버퍼의 유한성)
    - 더 생산하고 싶을 경우(생산자 입장에서 더 이상 사용할 수 있는 자원이 없는 상태)
    - 소비자 입장에서 더 이상 사용할 수 있는 데이터가 없는 경우

![](assets\03\bb(2).png)

- semaphore 변수(3가지)
  - mutex: lock을 걸기 위한 변수
  - semaphore full: 내용이 들어가있는 버퍼의 수
  - empty: 배용이 비어있는 버퍼의 수



### Readers-Writers Problem

![rw](assets\03\rw.png)

- 프로세스의 2종류
  - Read
  - Write
  - cf. DB == 공유 데이터를 의미
- 공유데이터(DB)에 동시에 접근하면 안된다.
- write는 동시에 하면 안되지만, read는 동시에 가능
- read시 write는 막아야 하지만, 동시에 read를 하는 것은 가능
- db: DB에 대한 락을 거는 바이너리 세마포어

![rw](assets\03\rw(2).png)

- readcount변수(read하는 프로세스의 수) : 1일 때 락을 걸어줌 -> 그 후에 필요 X
- readcount에 lock을 걸 변수 mutex
- writer들은 reader들이 다 빠져나가야할 때 까지 기다려야 함(현재의 케이스)
  - starvation 문제 발생 가능
  - queue에 우선 순위를 부여해서 문제를 해결할 수 있음(cf. 신호등)

