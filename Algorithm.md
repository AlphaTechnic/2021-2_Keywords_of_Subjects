# 1강

- 다양한 algorithm 문제들
  - 가짜 동전 찾기 -> binary search
  - 독이 든 술단치 -> bitmasking
  - Euler cycle : 모든 edge들 한번 씩 방문하는 cycle
  - Euler path : 모든 edge들 한번 씩 방문하는 path
  - 해밀턴 cycle(path) : 모든 vertext들 한번 씩 방문하는 cycle(path)
  - TSP(Traveling Salesman Problem) : HC인데, $\sum edge ~costs$가 최소인 거 찾기



# 2강

- 다양한 algorithm 문제들 이어서
  - minimum vertex cover
    - vertex cover : $S_{vc}$ s.t $S_{vc}$의 vertex들로 모든 edge들 다 cover
    - 모든 edge들이 $S_{vc}$의 vertex들에 incident
  - maximum independent p
    - $S_{ind}$ s.t $S_{ind}$의 어떤 두 vertex 쌍을 잡더라도 서로 이웃하지 않음
    - 어떤 두 vertex 쌍도 서로 adjacent하지 않음
  - maximum clique p
    - $S_{c}$ s.t $S_{c}$ 내의 어떤 두 vertex 쌍을 잡더라도 서로 이웃
    - 어떤 두 vertex 쌍도 서로 adjacent함
  - maximum 이분 매칭
    - 매칭 : vertex를 공유하지 않는 edge들의 집합
  - Stable matching p
    - unstable pair : 서로가 남의 짝을 더 탐내는 상황(불륜가능성 있는 매칭)
  - Graph coloring
    - k-coloring
    - 크로매틱 number finding(최소 색깔 찾기)
  - 냅색 p
    - fractional : 가성비 greedy
    - 0 - 1 : dp
- Problem
  - input(instance)
  - constraint
  - objective : cost를 최소화 혹은 최대화
- 시간 복잡도가 같은 경우 -> overhead(constraint factor) 고려
- 다항시간 알고리즘을 찾을 수 없는 경우 사용하는 방법들
  - brute force method : instance가 작은 경우
  - efficient search algorithm
    - 백트래킹
    - branch and bound(bfs)



# 3강

- 다항시간 알고리즘을 찾을 수 없는 경우 사용하는 방법들
  - 휴리스틱 알고리즘 (쓸만한 알고리즘)
    - 장점
      - 수행시간이 polynomial time이다
    - 단점
      - 모든 instance들에 대해 optimal은 아님
      - 알고리즘의 좋고 나쁨 판별이 어려움
  - Approximation 알고리즘
    - 'Ca가 1.5Copt 정도의 성능은낸다.' 정도 처럼 일정한 bound 내의 성능을 낸다고 증명된 알고리즘
  - Instance에 제한을 건다
    - Root finding -> 방정식의 형태를 제한(2차함수만 input으로 온다든가)
    - k - coloring
      - k <= 2로 제한 혹은
      - planar graph만 보겠다
    - sorting도 instance에 제한을 걸면 O(n)에 가능



- `Solution space` : brute force 방법으로 탐색할 때 생성되는 객체
- `feasible solution` : problem의 constraint는 만족
- `optimal solution` : feasible solution 중 objective 함수가 최소 또는 최대인 원소



- Mathmatical induction(수학적 귀납법)
  - 언제 씀? statment가 어떤 seq로 표시될 때
  - Steps
    - step1. Induction Base
    - step2. Induction Hypothesis
    - step3. Induction Step("by step2에 의하여 true"라는 문장이 반드시 있어야)



# 4강

- T(n), W(n), B(n), A(n)
- g(n) = O(f(n)) iff
  - $\exists c, n_0$ s.t $ n \ge n_0$ $\Rightarrow$ $cf(n) \ge g(n)$
    - ~이 O(n)임을 보여라. -> 적절한 $c, n_0$ 찾아주면 됨.
    - ~이 O(n)이 아님을 보여라. -> c는 positive value인데 어떻게 잡아도 안된다는걸 보여주면 됨
- g(n) = $\Omega(f(n))$ iff
  - $\exists c, n_0$ s.t $ n \ge n_0$ $\Rightarrow$ $g(n) \ge cf(n)$
- g(n) = $\Theta(f(n))$ iff
  - $\exists c1, c2, n_0$ s.t $ n \ge n_0$ $\Rightarrow$ $c_1f(n) \le g(n) \le c_2f(n)$
- g(n) = o(f(n)) iff
  - $\forall c, ~\exists n_0$ s.t $ n \ge n_0$ $\Rightarrow$ $cf(n)\ge g(n) $
  - 상한을 여유있게 잡아준 것
- `theorem`
  - g(n) = o(f(n)) 이면, g(n) = O(f(n)) but g(n) != $\Omega(f(n))$



