# System Structure & Program Execution Q&A

[toc]

## CPU & Memory & I/O device(컴퓨터의 3대 구성요소)

![컴퓨터시스템구조](assets/컴퓨터시스템구조.png)

### CPU

![wikimedia cpu 이미지](https://upload.wikimedia.org/wikipedia/commons/d/d8/ABasicComputer.gif)

- 중앙 처리 장치, 연산 담당

- CPU의 구성

  - (프로세스)레지스터: 연산에 필요한 데이터 저장(고속 저장 장소, 일반 메모리보다 훨씬 빠른 속도로 접근하도록 설계) (cf. 캐시 메모리는 CPU와 별도로 있는 공간)
    - 범용 레지스터: 연산과 데이터 전송에 주로 사용
    - 세그먼트 레지스터: 세그먼트라는 미리 할당된 메모리 영역의 시작 주소를 가리킴
      - CS(Code Segment): 코드 세그먼트의 시작 주소
      - SS(Stack Segment): 스택 세그먼트의 시작 주소
      - DS(Data Segment): 데이터 세그먼트의 시작 주소
      - ES(Extra Segment), FG, GS: 추가적인 데이터 세그먼트 레지스터
    - 명령어 포인터: 다음 실행할 명령의 주소
    - FLAG 레지스터: CPU 동작을 제어하거나 연산의 결과를 반영하는 개별적인 2진수 비트들로 구성
  - 제어부: 명령어의 해석과 올바른 실행을 위해 CPU 내부적으로 기계 명령어 실행 순서 제어
  - 산술 논리 연산장치: 덧셈/뺄셈 OR/AND/NOT과 같은 비교, 판단, 연산을 수행

- CPU의 동작(5단계)

  - 인출: 프로그램의 메모리에서 명령어를 불러오는 역할
  - 해독: 인출 단계에서 가져온 명령어를 해독하여 명령어 내의 데이터 정보와 연산 정보를 추출한 뒤, 중앙처리 내의 각 장치에 적절한 제어신호를 보내 연산, 처리에 대한 준비를 하는 단계
  - 실행: 명령어에서 추출한 두 데이터와 연산 정보를 이용해 실제로 연산하는 단계
  - 메모리: 연산결과가 다음 명령어에 바로 사용되지 않는다면 결과를 메모리에 저장
  - 라이트백: 이전 명령어의 연산 결과가 다음 명령어의 입력 데이터로 사용될 경우, 계산 결과를 레지스터에 다시 쓰는 것

- CPU의 성능

  - 클럭 속도
    - PU에서 클럭이라고 하는 수치는 중앙 처리 장치 내부에서 일정한 주파수를 가지는 신호로 이 신호에 동기화되어서 중앙 처리 장치의 모든 명령어가 동작
    - 클럭 주파수가 빠를수록 제한된 시간에 더 많은 명령 처리 가능
  - 코어의 수
    - 중앙 처리 장치의 역할 하는 블록
    - 종류
      - 싱글 코어: 하나의 코어로 이루어진 CPU
      - 멀티 코어: 한 개의 칩 안에 여러 개의 연산을 처리할 수 있는 장치를 병렬적으로 연결

- CPU는 메인보드에 있는 CPU 소켓에 부착된 핀을 통해 다른 부품들과 통신

  (버스 :  컴퓨터 안의 부품들 간에, 또는 컴퓨터 간에 데이터와 정보를 전송하는 통로(통신 시스템).  관련된 모든 하드웨어 부품들 및 통신 프로토콜을 포함한 소프트웨어)

  - 핀과 연결되는 부분

    (초창기의 컴퓨터는 단일 버스 구조. CPU, 메모리, 하드디스크, 주변장치들 사이의 속도 차가 점점 커져서 병목현상 심화. 이를 해결하기 위해 버스가 세분화될 필요성이 생겼고, 점점 컴퓨터의 버스는 세분화)

    - 데이터 버스: 데이터 전달
    - 제어 버스 : 제어 신호 전달
    - 주소 버스: 메모리 주소나 I/O Unit 포트 번호 전달



### Memory

- 주 기억 장치, 기억 담당
- 버스 : 데이터를 컴퓨터의 한 부분에서 다른 부분으로 전송
- 버스의 종류
  - 데이터 버스: CPU와 메모리 간에 명령어와 데이터 전송
  - 입출력(I/O) 버스: CPU와 입출력 장치 간에 데이터 전송
  - 제어 버스: 버스에 연결된 모든 장치의 동작을 동기화하기 위해 2진 신호 사용
  - 주소 버스: 현재 실행 중인 명령어가 CPU와 메모리 간에 데이터를 전송할 때에 명령어와 데이터의 주소를 가지고 있음
- 메모리 관리 기법
  - 가상 메모리 : 실제 메모리 주소가 아닌 가상 메모리 주소를 사용
    - 세그먼트 기법: 가상 메모리를 서로 크기가 다른 논리적 단위인 세그먼트로 나누는 것
    - 페이징 기법: 가상 메모리 서로 같은 크기의 블록으로 나누는 것



### I/O device 

입출력 장치(컴퓨터의 2차 부품), 컴퓨터 외부와 소통 담당

### cf. 프로세스





## System Call

운영 체제의 커널이 제공하는 서비스에 대해, 응용 프로그램의 요청에 따라 커널에 접근하기 위한 인터페이스

즉, 커널 모드와 사용자 모드로 나뉘어 구동되는 운영체제에서 커널을 사용자 모드, 즉 프로세스가 사용할 수 있도록 해주는 기능

#### 시스템 호출의 세 가지 기능

1. 사용자 모드에 있는 응용 프로그램이 커널의 기능을 사용할 수 있도록 한다.
2. 시스템 호출을 하면 사용자 모드에서 커널 모드로 바뀐다.
3. 커널에서 시스템 호출을 처리하면 커널 모드에서 사용자 모드로 돌아가 작업을 계속한다.

![https://ju-hy.tistory.com/8](https://blog.kakaocdn.net/dn/ALlGh/btquL0XgOow/qaDksq1AsUKrpZKEzSu0DK/img.png)



#### 시스템 호출의 유형

1. 프로세스 제어(process Control)
   - `exec()` : 다른 프로그램의 실행
   - `fork()` : 새 프로세스의 생성
   - `wait()` : 자식 프로세스가 끝날 때 까지 대기
2. 파일 조작(file manipulation)
   - `open()`, `read()`, `write()`
3. 장치 관리(Device Management)
4. 정보 유지(Information maintenance)
5. 통신(Communication)



## Interrupt

### Asychronous Interrupt(Hardware Interrupt)

- 비동기식 이벤트
- 다른 하드웨어 장치가 CPU와 상관없이 발생시킴
- keyboard event, i/O interrupt, timer ticks

### Synchronous Interrupt(Software Interrupt) (Exception)

- 동기식 이벤트
- 내부적으로 CPU control unit이 명령어의 실행 결과로 자주 발생시킴
- 0으로 나누기, page fault

### Trap

- 실행 중인 프로그램 내에 테스트를 위해 특별한 조건을 걸어 놓은 것





###### 참고

- CPU와 Memory 구조 https://d4m0n.tistory.com/12

- 중앙처리장치(위키 백과) https://ko.wikipedia.org/wiki/%EC%A4%91%EC%95%99_%EC%B2%98%EB%A6%AC_%EC%9E%A5%EC%B9%98

- 버스(컴퓨팅)(위키 백과) https://ko.wikipedia.org/wiki/%EB%B2%84%EC%8A%A4_(%EC%BB%B4%ED%93%A8%ED%8C%85)

<hr>

- 시스템 호출(위키 백과) https://ko.wikipedia.org/wiki/%EC%8B%9C%EC%8A%A4%ED%85%9C_%ED%98%B8%EC%B6%9C

- 시스템콜이란 https://velog.io/@woo0_hooo/%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91%EB%8C%80%EB%B9%84-System-Call%EC%9D%B4%EB%9E%80
- system call이란 https://ju-hy.tistory.com/8

<hr>

- 인터럽트와 예외 그리고 트랩의 차이 https://donghoson.tistory.com/1

- 인터럽트 https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8