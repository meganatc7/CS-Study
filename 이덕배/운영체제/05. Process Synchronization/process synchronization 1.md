# Process Synchronization 1

[toc]

## Critical section

![critical section](assets\01\critical section.png)

- **임계 구역**(critical section) 또는 **공유변수 영역**: 병렬컴퓨팅에서 둘 이상의 스레드가 동시에 접근해서는 안되는 공유 자원(자료 구조 또는 장치)을 접근하는 코드의 일부
- 두 개의 프로세스가 동시에 접근하지 않도록 만들기 위해 공유 데이터 접근 이전에 entry section을 통해 lock을 걸어 동시 접근을 막음



## 충족 조건

![충족조건](assets\01\충족조건.png)

1. Mutual Exclusion(상호 배제)

   > 어떤 프로세스가 이미 들어가 있으면 다른 프로세스는 들어가면 안된다.

2. Progress

   > 아무도 들어가있지 않은 상태에서 critical section에들어가고 싶으면 접근할 수 있게 해야한다.

3. Bounded Waiting

   > 기다리는 시간이 유한해야 한다. (특정 프로세스 입장에서 지나치게 오래 기다리는 starvation을 막아야 함)
   >
   > ex. 프로세스가 세개 있는 경우 둘이 번갈아가며 사용하고 하나는 배제되는 경우



## 해결 Algorithm

### Algo1

![algo1](assets\01\algo1.png)

- turn : 누구 차례인지를 말해주는 변수
- 본인의 차례가 아닌 경우 while 문에 들어가 대기 / 상대방에 critical section에서 나오면(차례를 바꿔줌) critical section에 들어갔다가 수행 후 턴을 바꿈
- progress 조건 만족 X => why? 무조건 교대로 하는 방식 -> 한쪽이 들어가지 않는다면 다른 한쪽은 영원히 못들어가는 경우 발생 => algo2



### Algo2

![algo2](assets\01\algo2.png)

- flag : 각각의 프로세스가 가지는 변수로, 본인이 critical section에 들어가고자 하는 의사표시
- 상대방이 의사를 가지고 있다면 양보하는 방식
- 둘 다 의사표시를 한 경우(flag를 든 경우) 서로에게 양보하는 문제 발생 => algo3



### Algo3

![algo3](assets\01\algo3.png)

- turn과 flag 변수 모두 사용
- 상대방이 의사도 있고 상대방 차례일 경우에만 기다림 -> 둘 중 하나라도 미충족시 내가 들어감
- 경우의 수를 다 따져보는 방식(조건 모두 충족)
- but, bust waiting(=spin lock!) : 상대방이 CPU를 잡은 경우 나는 계속 while문을 돌아야 함 => 비효율적(while문만 돌다 CPU 할당 시간을 다 쓰는 문제 발생 가능)❓❓❓



### Synchronization Hardware❓❓❓

![hardware](assets\01\hardware.png)

- 하드웨어적으로 하나의 instruction이 제공되면 위의 과정이 수월해질 수 있음
- 어떤 데이터를 읽고 쓰는 걸 하나의 instruction으로 처리할 수 없기에 CPU를 빼앗는 문제를 간단히 해결 가능
- ex. a == 0일 경우, 읽고 쓰고 a를 1로 바꿈. 이 과정에서 test_and_set만 lock을 확인하고 없다면 내가 lock을 함과 동시에 사용하면 됨
- 하드웨어적으로 값을 읽고 쓰는 걸 automatic하게 만들 수 있다면 lock을 걸고 푸는게 쉬어짐



cf) ❓❓❓

 ![semaphores](assets\01\semaphores.png)

- 프로그래머 입장에서 연산을 통해 lock을 걸고 푸는 걸 지원