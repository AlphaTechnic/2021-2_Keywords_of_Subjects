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
  - Utility-based agent (목적에 이르는 효율적인 비용도 생각하는 개념)



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
      - **check for redundant path**
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



- Informed Search
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

- `Admissible`
  - **heuristic이 admissible <=> never overestimates [goal까지 가는 비용]**
  - `Thm`
    - h(n)이 addmissible => A* using TREE-SEARCH is optimal
  - `tree search` vs `graph search`
    - graph search는 repeated state를 버림
- `Consistency` 
  - **heuristic이 consistent <=> h(n) $\le$ c(n, a, n') + h(n')**
  - `Thm`
    - **h(n)이 consistent => A* using GRAPH-SEARCH is optimal**
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
    - 아래는 space complexity를 해결해보려는 노력들



- **Weighted A* search**
  - Faseter, but optimal 보장 못함
- **Memory-bdd heuristic search**
  - "reached"(vis)에서 앞으로 안쓰게 될 거 메모리에서 지움
  - **Beam Search** 에서 branch factor 제한
  - **Iterative deepening A* (IDA*)**
  - **(Simplified) Memory-bdd A* ((S)MA*)**
    - child 중에서 너무 쓰레기인거는 버림
  - `RBFS` (Recursive-best-first-search)
    - `optimal` if h(n) is admissible
    - Space complexity : **O(bd)**



- problem의 relaxed version의 exact solution 을 휴리스틱으로 할 수도
  - 상하좌우로만 이동가능한 퍼즐블록들이 날아다닐 수도 있다는 식으로 제약 조건을 relax
- problem의 subproblem의 solution 을 휴리스틱으로 할 수도
  - 1~9까지 있는 퍼즐 블록을 1~4까지만 있고 나머지는 don't care로 생각한다거나



# 6강

- **(Greedy) Local Search**

  - suitable for optimization problems
  - 장점
    - 메모리 적게 씀
    - 답 빨리 찾음
  - 단점
    - local minimum에 빠질 수 있음

  

  - **Hill climbing search**
    - Stochastic HC
      - 현재 state보다 나은 이웃 state 중 하나를 랜덤하게 선택
    - First-choice HC
      - 좋아지는 거 첫 발견시 무지성 선택
    - Random-restart HC
      - 스타트를 랜덤하게 해 줌
  - **Simulated anealing**
    - local maximum을 빠져나오기 위해 일부러 bad move를 하용
      - 초반에는 온도 T를 뜨겁게해서, bad move를 높은 확률로 허용함
      - 후반으로 갈수록 온도 T를 점진적으로 낮춰서 bad move를 거의 허용하지 않음
    - but gradually decrease their freq
  - **Local Beam Search**
    - brach factor를 k개 정도로 제한
  - **Genetic algorithm**
    - 적자 생존, 돌연 변이 같은 요소를 알고리즘에 도입





# 7강

- **Adversarial Search**
  - MinMax
  - AlphaBeta Pruning
  - MCTS(Monte Carlo Tree Search)
    - evaluation function 구하는 데 비용이 크다면? => simulation 해서 승 / 패 통계를 다 구해보림



# 8강

- CSP
  - 특정한 상황이 변수를 제약하는 상황에서 그러한 제약 조건을 모두 만족시키는 변수의 쌍을 구하는 문제
  - 장점
    - constraint를 만족하도록 expand하기 때문에 search space의 많은 부분을 날려버릴 수 있음
  - Arc consistency
    - 노드 2개가 제약 조건을 만족시킴
    - X -> Y is `consistent` <=> for `every` value of X there is some allowed y (방향성이 있는 개념)

# 9강

- Backtracking Search
  - 가장 간단히 생각할 수 있는 무지성 search이고, 이를 개선시키는 방안을 생각해봄



- MRV(minimum remaining values)
  - fail-first 정책으로 선택해 감
  - variable이 고를 수 있는 선택지가 별로 없는 그 놈. 그 놈 우선 순위로 선택해간다.
- Degree heuristic
  - degree가 제일 큰 놈 우선순위로 선택해 간다.
- Least constraining value
  - fail-last 정책으로 선택해 감
  - 최대한 많은 선택지를 남기는 방향으로 expand해서 solution을 발견할 수 있도록 하는 idea

- Forward checking
  - filtering 사용해서 search 비용을 좀 줄인다.





# 10강

- **Local search for CSP**
  - 현재 state만 local하게 보고 min-conflict인 방향으로 expand한다.
  - 장점
    - 매우 큰 사이즈도 처리할 수 있을 정도로 효율적임
    - simulated annealing도 가능
  - constraint에 weight를 줄 수도 있음



그래프의 structure를 파악해서 Time complexity를 줄여줄 수도 있음

- **Tree-structured CSPs**

  - 루프가 없는 Tree 구조라면 CSP 해결 알고리즘의 시간 복잡도는 무려 O($nd^2$)이 됨

  - tree의 말단부터 root 직전(node2)까지 올라오면서, arc consistency 적용 `(RemoveInconsistent(parent(Xj)), Xj)`

  - root부터 말단까지 내려가면서, 값을 할당

    

  - **Nearly Tree-structed CSPs**

    - `cycle cutset`을 골라다가 특정 값을 assign -> 그러면 나머지가 tree가 됨.
    - 시간복잡도를 O($d^c (n - c)d^2$)로 줄어듦. linear
    - 그러나 `cycle cutset`을 찾아내는 게 쉽지 않음. NP-hard

  - **Join tree algorithm**

    - cluster로 노드들을 묶어서(decomposition) tree 구조로 만듦.
    - connected subproblems로 만드는 것.
    - 시간 복잡도는 O($nd^{w+1}$), n은 hypernode의 크기
    - 그러나 이렇게 join tree로 만드는 알고리즘이 NP-hard



# 11강

- Local Agent(knowledge-based agent)
  - partially observable한 환경에서 추리(reasoning)공정을 통해서 새로운 표현들을 유도함.
  - `tell`, `ask`



- Logical Inference
  - 알고리즘 i가 `sound`하다.
    - i is sound if whenever KB $\vdash_i \alpha$ it is also true KB $\vDash \alpha$
    -  알고리즘이 유효한 결과만 뽑아내더라
  - 알고리즘 i가 `complete`하다.
    - i is sound if whenever KB $\vDash \alpha$ it is also true KB $\vdash_i \alpha$
    - KB가 뽑아내는 것들을 알고리즘 i가 다 찾을 수 있다.
  - 위 둘은 별개의 개념. `sound`임과 동시에 `complete`해야함

-  Syntax
  - `automic sentences`($\approx$ literal)
  - 그들의 결합으로 complex sentences를 만듦. (S1 $\wedge$ S2 등)



- Application of inference rules

  - KB $\vDash (\alpha = \neg P_{1, 2})$ 와 같은 것을 판정할 때, 진리표 이용해서 M(KB) 찾고, M($\neg P_{1, 2}$) 찾고 하는 것은 너무 비효율적임 (Model checking)

    - 시간 복잡도가 O($2^n$)

  - 아래와 같은 rule을 통해 유도하면, 선형시간에 같은 결론을 낼 수 있음

    - **Modys Ponens**

      - $\frac {\alpha \Rightarrow \beta, ~ \alpha} {\beta}$

    - **And-elimination**

      - $\frac {\alpha \wedge \beta} {\beta}$

    - **Biconditional-elimination**

      - $\frac {\alpha \Leftrightarrow \beta} {(\alpha \Rightarrow \beta) \wedge (\beta \Rightarrow \alpha)}$

      

  

# 12강

- Application of inference rules
  - Resolution(분해)
    - $\frac {l_1 \lor l_2, ~ \neg l_2 \lor l_3} {l_1 \lor l_3}$
- CNF(Conjunctive Normal Form)
  - 모든 논리 문장은 **"절들의 논리곱"**으로 나타낼 수 있음
- Definite Clauses
  - 딱 1개의 positive literal이 있는 절
  - $(\neg L_{1, 1} \lor \neg Breeze \lor B_{1, 1}) \equiv (L_{1, 1} \land Breeze) \Rightarrow B_{1, 1}$
  - 위처럼 고치면, `Forward and Backward Chaining`(시간복잡도가 linear)을 적용할 수가 있음



- Forward Chaining
  - 위상정렬 비슷
  - algorithm은 complete하다.
  - data-driven
- Backward Chaining
  - bfs 역추적 비슷
  - goal-driven
  - sizeof(KB)보다 훨씬 사이즈 줄어듦



- Propositional Logic에서는 표현력에 한계가 있음
  - all 이나 some같은거
  - 시간 개념같은거



