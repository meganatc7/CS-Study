# 12 Replacement Strategies - Variable allocation

- **Working Set(WS) 알고리즘**

  - Locality에 기반을 둔다.

  - Working Set

    - 프로세스가 특정 시점에 자주 참조하는 page들의 집합
    - 최근 일정 시간동안 참조된 page들의 집함
    - 시간에 따라 변한다.
    - W(t, A): t에서의 working set, t-A 과 t사이의 참조된 page들의 집합
    - A: window size

  - Working set을 메모리에 항상 유지한다. => page fault rate 감소 => 시스템 성능 향상

  - window size(A)는 고정돼있다.

  - `Window size` vs `Working set size`(메모리 allocation)

    ![working set](img/working%20set.PNG)

    locality에 의해서 조금만 window size를 늘려도 참조하는 page 수가 많아진다.

    하지마 locality가 한정적이기 때문에 어느 시점을 지나면 program size는 둔화된다.

  - 적재되는 페이지가 없고 메모리를 반납하는 페이지가 있을 수 있다.

  - 새로 적재되는 페이지가 있고 교체되는 페이지가 없을 수 있다.

  - **지속해서 관찰해야하는 단점이 있다 => working set management overhead 발생**

    **=> page fault가 없더라도 지속적으로 관리해야 한다.** => Page Fault Frequency 알고리즘





- **Page Fault Frequency 알고리즘**
  - Residence set size를 page fault rate에 따라 결정한다.
    - page fault rate: Low(**long inter-fault time**) => Memory Allocation을 줄여준다. 
    - page fault rate: High(**short inter-fault time**)=> Memory Allocation을 늘려준다.
  - Resident set 갱신 및 메모리 할당 => page fault가 발생시에만 수행한다.
  - 알고리즘 과정
    - page fault가 발생 시 IFT(inter fault time)으 계산한다.
    - IFT > threshold value
      - residence set동안 참조된 page들만 유지하고 나머지 page들은 메모리에서 내린다.
    - IFT < threshold value
      - 기존 pages들은 유지한다.
      - 현재 참조된 page를 추가로 적재한다.



- **Variable MIN algorithm**

  - 평균 메모리 할당량과 page fault 발생 횟수 모두 고려했을 때의 Optimal

  - 페이지 참조 string을 미리 알고 있어야 한다. => 실현 불가능한 기법

  - 알고리즘

    - page r이 t시간에 참조되면, (t, t+A] 사이에 다시 참조되는지 확인한다.
    - 참조된다면 page r을 유지하고, 참조되지 않을 경우 page r을 메모리에서 내린다.

  - 그렇다면, 최적 성능을 위한 A값은 어떻게 될까?

    - A = R (Page fault 발생 시 처리 비용) / U (한번의 참조시간동안 page를 메모리에 유지하는 비용)

    - R > A * U => 처리비용이 더 크다 => A를 늘려준다.
    - R < A * U => 유지비용이 더 크다 => A를 줄여준다.
