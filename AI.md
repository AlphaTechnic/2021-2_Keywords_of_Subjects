# 1강

- Intelligence

  perception, action, reasoning, communication, planning

- Artificial Intelligence

  - weak
  - strong, human-level, general



- Acting rationally로 가야된다.

  - optimal solution



# 2강

- Agent : Perceives and acts (Architecture + Program)
  - Rational agent : do the right thing
- Rationality
  - explore (넓게), exploit (깊게)
- Rational agent 디자인을 위해 task environment를 구체화
  - PEAS (자동 택시를 예시로)
    1. Performance measure : 안전성, ..
    2. Environment : 보행자, 날씨, ..
    3. Actuators (구동) : 브레이크, 악셀레이터, 스피커, ..
    4. Sensor : 속도계
- agent 종류
  - Table lookup agent
  - simple reflex agent
  - Model-based agent : state, action
  - Goal-based agent
  - Utility-based agent



# 3강

- Search 문제를 정의하는 5가지 요소
  - initial state
  - action
  - transition model
  - goal test
  - path test



- Search Algoritms
  - Tree search vs Graph search
    - Tree search
      - 새로운 state를 밑에 하나씩 붙여가면서(expand) 탐색
      - tree size를 키워가면서 탐색함
      - 봤던 state를 또 방문하면서 무한루프에 빠질 수 있음
    - Graph search
      - check for redundant path
      - `closed` : 방문 체크(`visited`)
      - `fringe` : expand된 애들(`que`)

  

- Search의 Performance measure

  - `Completeness` : solution이 존재한다면 무조건 찾느냐
  - `Optimality` : 주는 solution이 optimal이냐
  - `시간 복잡도`
  - `공간 복잡도`



- terminology
  - `b` : (maximum) branching factor
  - `d` : shallowest solution
  - `m` : maximal length



- Uniformed search (Blind search)
  - BFS
    - Uniform cost search (다익스트라)
  - DFS
    - Depth-limited search
    - Intrative deepening search
  - Bidirectional search



# 4강

- 큰 얼개
  - Uninformed search (Blind search)
    - BFS
      - (응용) UFS
    - DFS
      - (응용) DLS
      - (응용) IDS
    - Bidirectional Search



- Details

|           | BFS      | UFS                                 | DFS      | DLS      | IDS      | Bi                 |
| --------- | -------- | ----------------------------------- | -------- | -------- | -------- | ------------------ |
| complete? | yes      | yes                                 | yes      | no       | yes      | yes                |
| optimal?  | yes      | yes                                 | yes      | no       | yes      | yes                |
| time      | O($b^d$) | O($b^{1 + \frac {C^*} {\epsilon}}$) | O($b^d$) | O($b^l$) | O($b^d$) | O($b^{\frac d 2}$) |
| space     | O($b^d$) | O($b^{1 + \frac {C^*} {\epsilon}}$) | O($bm$)  | O($bl$)  | O($bd$)  | O($b^{\frac d 2}$) |



- A* algorithm

  - 최단 경로 문제를 푸는 효율적인 알고리즘

  - `evaluation function` : $f(x) = g(x) + h(x)$

  - 다익스트라 vs A*

    - 다익스트라

      ```python
      adj_graph = [[0 for _ in range(V)] for _ in range(V)]
      
      pre = [0 for _ in range(V)]
      dist = [INF for i in range(V)]
      dijkstra(S)
      path = get_path(S, TAR)
      ```

    - A*

      - 각 정점 간의 추정거리($h(v)$)를 알 수 있다고 가정
      - Search 알고리즘에 `방향성`($h(v)$가 짧은 방향)을 부여해서 진행할 수 있음

      ```python
      adj_graph = [[0 for _ in range(V)] for _ in range(V)]
      
      # heuristic function 정의    
      h = [0 for _ in range(V)]
      for _ in range(V + 1):
          a = map(int, input().rstrip().split())
          h_val = Manhattan_dist(a, tar)
          h[a] = h_val
      
      pre = [0 for _ in range(V)]
      dist = [INF for i in range(V)]
      a_star(S)
      path = get_path(S, TAR)
      
      ```



# 5강

- Admissible
  - heuristic이 admissible <=> never overestimates [goal까지 가는 비용]
  - `Thm`
    - h(n)이 addmissible => A* using TREE-SEARCH is optimal
  - `tree search` vs `graph search`
    - graph search는 repeated state를 버림
- Consistency 
  - heuristic이 consistent <=> h(n) $\le$ c(n, a, n') + h(n')
  - `Thm`
    - h(n)이 consistent => A* using GRAPH-SEARCH is optimal
  - `Thm`
    - consistent => admissible



- A* 특성
  - A* expands all nodes with f(n) < C*(optimal path cost)
  - A* expands some nodes with f(n) = C*
  - A* expands no nodes with f(n) > C*
- 평가
  - completeness? Yes
  - optimal? Yes
  - Time complexity O($b^d$)
  - Space complexity O($b^d$)
    - Space complexity가 줜네 비싸다보니, 이거시 major problem이 된다.



- Weighted A* search
  - Faseter, but optimal 보장 못함
- Memory-bdd heuristic search
  - "reached"(vis)에서 앞으로 안쓰게 될 거 메모리에서 지움
  - Beam Search 에서 branch factor 제한
  - Iterative deepening A* (IDA*)
  - (Simplified) Memory-bdd A* ((S)MA*)
    - local에서 너무 쓰레기인거는 버림
  - `RBFS` (Recursive-best-first-search)
    - optimal if h(n) is admissible
    - Space complexity : O(bd)



- problem의 relaxed version의 exact solution 을 휴리스틱으로 할 수도
- problem의 subproblem의 solution 을 휴리스틱으로 할 수도



