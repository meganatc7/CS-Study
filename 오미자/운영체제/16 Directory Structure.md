# [16] Directory Structure

### [16.1] Flat Directory Structure 

flat => 평평한 => 계층이 없는 디렉토리이다.

파일시스템 내에 하나의 directory만 존재하는 구조이다.

![파일시스템-1](img/%ED%8C%8C%EC%9D%BC%EC%8B%9C%EC%8A%A4%ED%85%9C-1.PNG)



#### 문제점

- 파일 이름 충돌 횟수가 많아져서 이름 짓기가 어려워진다.
- 파일 관리(분류, 보관 등)가 어려워진다.
- 다중 사용자 환경에서 문제가 더욱 커진다.



### [16.2] 2-Level Directory Structure

flat보다 레벨이 하나 더 증가된 구조이며 사용자마다 하나의 directory를 배정한다.



#### 문제점

- Sub-directory 생성이 불가능하다.

- 파일을 공유하는데 이슈가 발생한다.
  - user1이 user2에게 특정 파일을 공유할 때, 전체 파일이 노출되게 된다.





### [16.3] Hierarchical Directory Structure 

- Tree 형태의 계층적인 directory 사용 가능하다.

- 사용자가 하부 directory 생성/관리가 가능하다
  - OS를 통해 System call로 진행된다.
- 대부분의 OS가 사용한다.





### [16.4] Acyclic Graph Directory Structure

- Hierarchical directory structure 확장버전으로 Cycle을 허용하지 않는다.
- Directory 안에 `shared directory`, `shared file`을 담을 수 있다.

- **Link** 의 개념을 사용한다. (ex) 바로가기 버튼

![파일시스템-2](img/%ED%8C%8C%EC%9D%BC%EC%8B%9C%EC%8A%A4%ED%85%9C-2.PNG)







### [16.5] General Graph Directory Structure

- Acyclic Graph Directory Structure의 일반화
  - Cycle을 허용한다.



#### 문제점

- 파일 탐색 시, infinite loop가 발생할 수 있다. 