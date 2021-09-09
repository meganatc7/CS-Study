# File System Implementation

[toc]

## 디스크에 파일을 저장하는 방법

![image-20210909213628439](assets/02/image-20210909213628439.png)

- 파일은 크기가 균열하지 않지만, 디스크를 동일한 크기로 나눠 섹터 단위로 이용
- 각각의 블록 = 논리적인 블록
- 메모리 관리의 페이징 기법과 유사



### Contiguous Allocation

- 연속된 방법
- 단점
  - 외부조각 발생 가능(비어있는 공간보다 파일들의 길이가 길다면, 빈공간 발생)
  - file grow가 어려움(제약이 존재함, 뒤의 빈 블록을 고려해야 함)
  - 파일 크기가 커질 때를 고려해 빈 공간을 준다면 내부 조각 발생(할당 되었는데 사용되지 않는 공간 발생)
- 장점
  - 빠른 I/O 가능(접근 시간을 줄일 수 있음)
  - swapping 용도로 좋음(공간 효율성보다 시간 효율성이 중요하기 때문, 금방 지워질 것)
  - real time 용
  - 직접 접근 가능(앞을 걸치지 않고 앞에서부터 5번째 위치한 블록으로 바로 접근 가능)

![image-20210909213718853](assets/02/image-20210909213718853.png)

![image-20210909214156584](assets/02/image-20210909214156584.png)



### Linked Allocation

- 연속적으로 할당하는 것이 아닌 빈공간에 할당하는 것
- 시작위치만 디렉토리에 저장하고, 디스크에 다음 위치 저장
- 장점
  - 외부 조각 발생 X
- 단점
  - 직접 접근 불가능(앞의 위치를 다 탐색해야 함)
  - reliability 문제 : 한 sector가 유실되면 그 뒤에도 유실
  - 다음 위치를 저장해야 하기 때문에 공간 효율성이 떨어짐

![image-20210909214640963](assets/02/image-20210909214640963.png)

![image-20210909214825223](assets/02/image-20210909214825223.png)

#### FAT(File allocation table)

- Linked Allocation을 활용하되, 공간 효율성을 높인 방법(뒤에 참조)



### Indexed Allocation

- 디렉토리에 인덱스 정보를 저장

- 장점

  - 직접 접근 가능
  - 외부 조각 발생 X

- 단점

  - 아무리 작은 파일이더라도 두 개의 블록 필요(인덱스 저장 블록/실제 데이터 저장 블록)

  - 굉장히 큰 파일일 경우 하나의 인덱스 파일로 표시 불가 

    cf. linked schema(인덱스 마지막에 다음 인덱스 위치 저장) / multi-level index(인덱스 안의 데이터가 또 다른 인덱스 위치를 가르키게 만드는 것) 사용

![image-20210909215257058](assets/02/image-20210909215257058.png)

![image-20210909215542830](assets/02/image-20210909215542830.png)



## 실제 시스템에서 어떤 파일 시스템을 어떻게 쓰는가?

### UNIX 파일시스템의 구조

- Partition(=Logical Disk)
  - Boot block(어떤 파일 시스템이건 가장 먼저 나옴)
  - Super block : 파일 시스템에 대한 총체적인 정보(어디가 빈 블록이고 어디가 사용중인 블록인지 그리고  inode list 데이터 정보)
  -  Inode list : 실제 파일의 메타데이터가 있는 위치(파일의 위치 정보는 index allocation 사용)
    - 크기에 따라 위치 정보 구성(direct(파일 위치) / single indirect (인덱스-파일 위치)/ double indirect(인덱스-인덱스-파일위치))
  - Data block : 파일의 이름은 디렉토리가 가지고 있음

![image-20210909215822221](assets/02/image-20210909215822221.png)

![image-20210910005427846](assets/02/image-20210910005427846.png)



### FAT File System

- 직접 접근이 가능하다!(FAT이라는 작은 테이블 내에서 확인하는 것이기 때문에)
- Linked allocation의 한계를 모두 극복한 것

- Partition(=Logical Disk)
  - Boot block
  - FAT : 파일의 메타 데이터 중 일부(위치 정보만, 나머지는 디렉토리에)
    - data block 개수만큼 존재(다음 블럭을 가르킴)
  - Root directory
  - Data block

![image-20210910010252457](assets/02/image-20210910010252457.png)

