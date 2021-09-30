# [17] File Protection

File에 대한 부적절한 접근을 방지하는 것이다

- 다중 사용자 시스템에서 더욱 필요하다!



**접근 제어가 피요한 연산들**

- READ
- WRITE
- EXECUTE
- APPEND





## [17.1] File Protection Mechanism (파일 보호 기법)

파일 보호 기법은 system size 및 응용 분야에 따라 다를 수 있다.



### [17.1.1] Password 기법

- 각 file들에게 pw를 부여한다.
- 비현실적이다.
  - 사용자들이 파일 각각에 대한 pw를 기억해야 한다.
  - 접근 권한 별로 서로 다른 pw를 부여해야 한다.



### [17.1.2] Access Matrix 기법 (접근 권한을 표에 적는다.)

- 범위(domain) 와 개체(object) 사이의 접근 권한을 명시한다.

- 용어정리

  - Object - 접근 대상(file, device 등)
  - Domain - 접근 권한의 집합, 같은 권한을 가지는 그룹(사용자, 프로세스)

  - Access right - <object 이름, 권한>

![17.1.2 access matrix](img/17.1.2%20access%20matrix.PNG)



#### 구현방법

- **Global Table**

  시스템 전체 file들에 대한 권한을 table로 유지한다.

  | Domain name | Object name | Right-set |
  | ----------- | ----------- | --------- |
  |             |             |           |

  - **간단하지만 테이블 사이즈가 커질 경우 관리하기 힘들고, 빈 공간이 생겨 메모리 낭비가 있을 수 있다.**

  

- **Access List**

  Access matrix의 열을 list로 표현한 것으로, 각 object에 대한 접근 권한을 나열한다.

  (ex) {<D1, R1>, <D2, R2>, ...}

  Object 생성 시, 각 domain에 대한 권한을 부여하며 Object 접근 시 권한을 검사한다.

  실제 os에서 많이 사용된다. (unix)

  - **object별 권한 관리가 용이하다는 장점이 있지만, 모든 접근마다 권한 검사를 해야하기 때문에 Object가 많이 접근하는 경우 느리다는 단점이 있다.**

  

- **Capability List (like 신분증)**

  Access matrix의 행을 list로 표현한 것으로, 각 domain에 대한 접근 권한을 나열한다.

  (ex) {>F1. R1>, <F2, R2>, ...}

  Capability를 가짐이 권한을 가짐을 의미한다. (프로세스가 권한 제시, 시스템이 검증 승인)

  시스템이 capability list 자체를 보호해야한다. - Kernel안에 저장한다.

  - **List내 object들에 대한 접근에 유리하다는 장점이 있지만, object별 권한 관리가 어렵다는 단점이 있다.**

  

- **Lock-key Mechanism**

  Access list와 Capability list를 혼합한 개념이다.

  Object는 Lock을, Domain은 key를 가진다.

  시스템은 key list를 관리해야 한다.

  