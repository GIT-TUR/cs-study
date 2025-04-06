# 디스크 스케줄링 질문 정리

<details>
  <summary><strong>디스크 엑세스 시간은 어떤 값들로 이루어져있는지 각각에 대해 설명해주세요.</strong></summary>
    1. 탐색 시간 : 읽고자하는 실린더까지 헤드가 이동하는 데 걸리는 시간</br>
    2. 회전 지연 시간 : 디스크가 회전하여 원하는 섹터가 헤드 아래에 도달할 때까지의 시간</br>
    3. 전송 시간 : 데이터를 실제로 읽거나 쓰는 데 걸리는 시간 
</details>
<details>
  <summary><strong>디스크 스케줄링의 목표는 무엇이 있나요?</strong></summary>
    탐색 시간 최소화
    <details><summary><strong>디스크스케줄링 알고리즘인 SCAN과 LOOK의 차이는 무엇인가요?</strong></summary>
        SCAN은 디스크의 끝까지 갔다가 오고, LOOK은 요청 범위 내만 움직여서 더 실용적
    </details>
    <details><summary><strong>디스크 스케줄링에서 탐색 시간이란 무엇인가요? 이 개념이 성능에 미치는 영향에 대해 설명해주세요.</strong></summary>
        디스크 헤드가 현재 위치에서 목표 트랙으로 이동하는 데 걸리는 시간으로 헤드의 이동거리가 탐색시간이 된다. 그래서 이 이동거리가 짧을수록 I/O성능이 좋아져 스케줄링 알고리즘은 이 이동거리를 최소화하고자 한다.
    </details>
</details>
<details>
  <summary><strong>FCFS 스케줄링의 장단점은 무엇일까요?</strong></summary>
    요청 순서대로 처리하니까 기아상태가 없고, 간단하지만 헤드 이동거리가 증가하면 탐색시간이 증가하여 성능이 저하된다.
    <details>
    <summary><strong>SSTF 스케줄링의 장단점은 무엇일까요?</strong></summary>
        현재 헤드에서 가장 가까운 요청을 우선 처리하여 헤드 이동 거리를 최소화하니까 성능이 좋지만 기아 가능성이 있다.
    </details>
</details>
