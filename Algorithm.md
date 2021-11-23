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
  - 역은 성립 안 함. (g(n) = 짝이면 n 홀이면 1 이런식으로 하면)



# 5강

- 알아두면 유용한 complexity 관련 사실
  - g(n) = O(f(n)) $\Leftrightarrow$ f(n) = $\Omega(n)$
  - g(n) = $\Theta(n)$ $\Leftrightarrow$ f(n) = $\Theta(g(n))$
  - $log_2n = log_3n$
  - $2^n << 3^n <<n!$
  - g(n) = O(f(n)), h(n) = $\Theta(f(n))$ => g(n), h(n)의 lin combi = $\Theta(f(n))$



- Decision Problem (결정문제)
  - `NP` : non-deterministic 알고리즘으로 polynomial time에 chk되는 문제
  - `P` : polynomial time에 해결되는 문제
  - `NPC` : polynomial time에 해결될지 말지를 모르는 문제



- Dynamic Allocation
  - 정리 : https://alphatechnic.tistory.com/35



- Singly Linked List

  - Storage Pool을 이용한 SLL 메모리 관리

    

    | application | <- allocSLL() | storage pool                    | -> malloc() | Sytem |
    | ----------- | ------------- | ------------------------------- | ----------- | ----- |
    | program     | -> freeSLL()  | 미사용 SLL을 linked list로 보관 | <- free()   | MEM   |



- C codes for Storage Pool

``` c
// global 변수
SLL* SLL_pool = NULL; // 이게 head
unsigned long SLL_cnt = 0;
unsigned long UsedMemoryForSll = 0;
```

- 함수 1. `SLL *allocSLL(void)`

```c
SLL *allocSLL(void){
  SLL* p;
  
  if (pool 비었으면) {
    malloc으로 받아옴
  } 
 	else{
    pool에서 원소하나 뺌
  }
  p -> p = NULL;
  ++SLL_cnt;
  return p;
}
```

- 함수 2. `void freeSLL(SLL *p)`

```c
void freeSLL(SLL *p){
  if (p -> i == NULL) 너 왜 이미 free한거를 또 free할라고 그러냐? return;
    
  p -> i == NONE;
  원소로 받은 p를 pool에 집어넣음
  --SLL_cnt;
}
```

- 함수 3. `void freeSLL_pool(void)`

```c
void freeSLL_pool(void){
  SLL* p = SLL_pool;
  p로 pool 쭈욱 순회하면서, free 조져벌힘.
    
  if (SLL_cnt != 0 ) 오류
}
```



- 스택 구현

- 함수 1. `void pushSLL(SLL **ST, SLL *p)`

```c
void pushSLL(SLL **ST, SLL *p){
  p -> p = *ST;
  *ST = p;
}
```

- 함수 2. `SLL* SLL popSLL(SLL** ST)`

```c
SLL* SLL popSLL(SLL** ST){
  SLL *p = *ST;
    
  if (size == 1) {}
  else {}
  return p;
}
```



- Queue 구현

- 함수 1. `void enqueueSLL(SLL **Q, SLL **Q_end, SLL* p)`

```c
void enqueueSLL(SLL **Q, SLL **Q_end, SLL* p){
  if (size == 0){}
  else {꼬리에 넣음}
}
```

- 함수 2. `SLL* dequeSLL(SLL** Q, SLL* Q_end)`

```c
SLL* dequeSLL(SLL** Q, SLL* Q_end){
  SLL *p = *Q;
  
  if (size == 1){}
  else {}
}
```





# 6강

> `classSLL.h`

```cpp
typedef struct _SLL{
  int i;
  struct _SLL *p;
}SLL;

class SLList{
  private:
  	static SLL* SLL_pool;
  	static unsigned long SLL_cnt;
  	static unsigned long UsedMemoryForSLLs;
  public:
  	SLL* allocSLL(void);
  	void freeSLL(SLL* p);
  	void freeSLL_pool(void);
};
```

> `classSLL.cpp`

```cpp
SLL* SLList::SLL_pool;
unsigned long SLList::SLL_cnt;
unsigned long SLList::UsedMemoryForSLLs;

SLL* SLList::allocSLL(void){
  // c와 동일
}
void freeSLL(SLL* p){
  // c와 동일
}
void freeSLL_pool(void){
  // c와 동일
}
```



> `Stack.h`

```cpp
class sllStack:public SLList{
  private:
  	SLL* ST;  // header
  public:
  	sllStack(void){  // 생성자
      ST = NULL;
    }
  	~sllStack(void){ // 소멸자
     while(!empty()){
       SLL *p = pop();
       freeSLL(p);
     } 
    }
  
  void push(SLL *p);
  SLL *pop(void);
  bool empty(void);
  SLL* top(void);
}
```



> `Stack.cpp`

```cpp
void sllStack::push(SLL *p){ // header 불필요
  //
}

void sllStack::pop(void){ // header 불필요
  //
}

void sllStack::empty(void){ // header 불필요
  //
}

```



> `Queue.h`

```cpp
class sllQueue:public SLList{
  private:
  	SLL *Q, *Q_end;
  public:
  	sllQueue(void){ // 생성자
      Q = Q_end = NULL;
    }
  	~sllQueue(void){
      while(!empty()){ // 소멸자
        SLL *p = deque();
        freeSLL(p);
      }
    }
  	
  	void enque(SLL *p);
  	SLL* deque(void);
  	bool empty(void);
  	SLL* top(void);
}
```

> `Queue.cpp`

```cpp
void sllQueue::enque(SLL *p){
  //
}

SLL* sllQueue::deque(void){
  //
}

bool sllQueue::empty(void){
  //
}

```





이제 Graph Implementation

- adjacent matrix
- adjacent list
- Using Linked List

```cpp
typedef struct _SLL{
  int i;
  struct _SLL *p
}SLL;

// vertex
typedef struct _vertex{
  SLL *p;
}

// edge
typedef struct _edge{
  int cost;
  int vf, vr;
}
```





# 7강

- Graph Implementation using Array













# 8강

> BFS

```python
def bfs(s):
  que = deque(s)
  vis = [False for _ in range(V + 1)]
  vis[s] = True
  while que:
    cur = que.popleft()
    # 여기에 vertex cost 관련 처리
    for nxt in graph[cur]:
      if vis[nxt]: continue
      
      # 여기에 edge cost 관련 처리 (cur ~ nxt)
      que.append(nxt)
      vis[nxt] = True
```



> DFS

```python
def dfs(cur):
  vis[cur] = True;
  # 여기에 vertex cost 관련 처리
  for nxt in graph[cur]:
    if vis[nxt]: continue
    # 여기에 edgecost 관련 처리 (cur ~ nxt)  
      
    dfs(nxt) 
```



- Euler Cycle
  - **자료구조**를 어떻게 설계하느냐에 따라, 효율적인 **알고리즘**으로 가느냐 마느냐가 될 수 있다.
  - **자료구조의 알고리즘으로의 영향력**
  - Euler Cycle :  모든 vertex deg가 짝수
  - Euler path : 모든 vertex deg가 짝수, 단 2개의 vertex deg는 홀수

> `DBL structure`

```cpp
typedef struct _DBL{
  int d;
  struct _DBL *twin;  // 다른 위치에 있는 나 자신을 가리키는 pointer
  struct _DBL *lp, *rp;
}
```

> `Class for DBL pool`

```cpp 
class DBList {
  private:
  	DBL *DBL_pool;
  public:
  	unsigned long DBL_cnt;
  	unsigned long UsedMemoryForDBLs;
  	DBList(void) {
      DBL_pool = NULL;
      DBL_cnt = 0;
      UsedMemoryForDBLs = 0;
    }
  	~DBList(void){
    }
  
  	DBL *allocDBL(void);
  	void freeDBL(DBL *p);
  	void freeDBL_pool(void);
}
```

> 함수 1. `DBL *DBList::allocDBL(void)`

```cpp
DBL *DBList::allocDBL(void){
  DBL *p;
  if (DBL_pool == NULL){
    (System MEM에서 가져옴)
  }
  UsedMemoryForDBLs += sizeof(DBL);
  p->d = NONE;
  else {
    (DBL_pool에서 하나 뺌)
  }
  
  p -> rp = p -> lp = p -> twin = NULL;
  ++DBL_cnt;
  return p;
}

```

> 함수 2. `void DBList::freeDBL(DBL *p)`

```cpp
void DBList::freeDBL(DBL *p){
  if (p -> d == NONE) (왜 이미 free인걸 또다시 free하려하는가) return;
  
  p -> d = NONE;
  p -> rp = DBL_pool;
  DBL_pool = p;
  --DBL_cnt;
}
```

> 함수 3. `void DBList::freeDBL_pool(void)`

```cpp
void DBList::freeDBL_pool(void){
  DBL *p = DBL_pool;
  while (p != NULL) {
    (pool 쭈욱 돌면서 free)
  }
  if (DBL_cnt) != 0 {(먼가 잘못됨!)}
}
```



# 9강

> `class dblStack` (graph의 ajfacent list 구성에 사용)

```cpp
class sblStack {
  private:
  	DBL *ST;
  public:
  	dblStack(void){
      ST = NULL;
    }
  	~dblStack(void) {
    }
  
  	void push(DBL *p);
  	DBL* pop(void);
  	void remove(DBL *p);
  	DBL *top(void);
  	void empty(void);
}
```

> `void dblStack::remove(DBL *p)`

```cpp
void dblStack::remove(DBL *p){
  if (p == ST){ // p가 헤드에 있으면,
    (제거)
  }
  else{ // 헤드가 아니라 다른 데 있으면,
    (제거)
  }
}
```



- 자료구조 구성을 완료했으니 -> 이제 구현 (O(E)에 가능해짐)

```cpp
typedef struct _Vertex{
  dblStack S;  // adj list contains edge index
  int degree;
}Vertex;

typedef struct _Edge{
  int v1, v2;
}Edge;
```



- Pseudo code (dfs와 상당히 흡사함)

```cpp
빈 stack stk와 크기가 V + 1인 배열 path를 준비;
S.push(start);
while (S != empty){
  cur = S.pop();
  if (deg(v) == 0){
    v를 path에 추가하고, stk에서 pop; 
  }
  else{
    for nxt in graph[cur]{
      1. e 삭제
      2. stk.push(nxt)
    }
  }
}
```





// 이제 Divide and Conquer로 진입.

// 이 알고리즘의 시간복잡도를 얻어내기 위해, 점화식 -> 일반항 바꾸는 법을 알 필요가 있다.



- Homogeneous Linear Recurrence Equation
  - 특성방정식(Characteristic eq) 이용
  - change of variable
  - substitution method

- Master method
  - 대충 T(n) = `a`T(n / b)일 때, `a`가 작냐 크냐에 영향을 많이 받음.



# 10강

> `mergesort()`

```c
void mergesort(int n, keytype S[]){
  if (n == 1) return;

  h = n / 2;
  m = n - h;
  U[1, .., n];
  V[1, .., n];
  cpy(S) to U, V 절반씩;
  
  mergesort(h, U);
  mergesort(h, V);
  mergesort(h, m, U, V, S);
}
```

=> function call 흐름이 dfs()랑 비슷할 수 밖에 없음. 다만 끝까지 간 뒤 merge() 작업 하나 추가된 셈



> `merge()`

```c
void merge(h, m, const keytype U[], const keytype V[], const keytype S[]){
  idx i = j = k = 1;
  while (i <= h && j <= m) { // i, j는 둘 중 하나만 증가, k는 항상 증가
    if (U[i] <= V[j]) { // 등호를 박아야 Stable을 유지할 수 있음
      S[k++] = U[i++];
    }
    else {
      S[k++] = V[j++];
    }
  }
  
  if (j <= m){ // j가 끝까지 가지 몬함
    cpy(V[j ~ m]) to S[k ~ (h + m)];
  }
  else{ // i가 끝까지 가지 못함
    cpy(U[i ~ h]) to S[k ~ (h + m)];
  }
}
```

=> 이 알고리즘은 추가적인 메모리로 S[] 외에 2n을 더 요구하게 됨. 이걸 n으로 줄일 수 있음



> `merge2()`

```c
void merge2(idx low, ldx mid, idx high){ // S는 글로벌로 있음
  idx i, j, k;
  keytype tmp[low,..high];
  i = low;
  j = mid + 1;
  k = low;
  
  while (i <= mid && j <= high){ // S를 tmp에 박음 (merge1()이랑은 반대)
    if (S[i] <= S[j]){
      tmp[k++] = S[i++];
    }
    else {
      tmp[k++] = S[j++];
    }
  }
  
  if (j <= high){ // j가 끝까지 못감
    cpy(S[j ~ high] to tmp[k ~ high];
  }
  else{
    cpy(S[i ~ mid]) to tmp[k ~ high];
  }
  cpy(tmp[low ~ high]) to S[low ~ high];
}
```

=> 어쨌건 n의 extra memory가 필요하기 때문에 **in-place sorting 알고리즘**이 아니다.

=> mergesort()는 등호를 박아줌으로써, **stable**(key값이 같은 경우 순서가 유지되는)을 유지할 수 있다.



- quicksort()

```c
void quicksort(idx low, idx high){
  if (low >= high) return;
  
  idx piv_point
  partition(low, high, piv_point);
  quicksort(low, piv_point - 1);
  quicksort(piv_point + 1, high);
}
```

> `partition`

```c
void partition(idx low, idx high, idx& piv_point){
  idx i;
  idx j = low; // j는 piv_itm보다 작은 놈들 모임의 오른쪽 끝을 가리키고 있기 위한 용도
  keytype piv_itm = S[low];
  
  for (i = low + 1; i <= high; i++){
    if (S[i] < piv_itm){ // 왼쪽으로 땡겨올 itm 발견..!
      j++;
      xchg(S[i], S[j]) // S[i]를 왼쪽으로 땡겨온다는 의미가 강하다.
    }
  }
  
  // 마무리
  piv_point = j;
  xchg(S[low], S[piv_point]);
}
```



- **Remark**
  - Time Complexity
    - worst case : $\Theta(n^2)$
    - average case : $\Theta(nlogn)$
    - but 이름처럼 줫네 빠르다고 알려짐
  - Space complexity
    - In-place algorithm (swap 때문에 (O(1)의 여분 하나 필요하긴 한듯?))
  - Stability
    - not stable
    - stable을 유지하고 싶으면 추가 메모리가 필요함
  - 순수한 quicksort()는 최악의 경우 depth를 n만큼 타고 들어갈 수 있어서 stackoverflow 위험 있음



- 행렬곱셈 (Strassen's 알고리즘)
  - 7개의 곱을 미리 계산하고, 분할정복을 적용한다.
  - 8개의 곱셈에서 곱셈을 딱 하나 줄였고, 덧셈이 무지 늘어났음에도 불구하고, $O(n^3)$따리를 $(O(n^{2.81}))$ 정도까지 줄여놓을 수 있음



- Large number에 대한 곱셈에 분할정복 적용
  - 분할 정복을 적용하기 위해 large number를
  - $x * 10^{n/2} + y$ 같은 느낌으로 봐주면, 4번의 곱셈을 3번까지로 줄일 수가 있다.



# 11강

- Large number 곱셈 분할정복 algorithm

```c
large_int prod(large_num u, large_num v){
  large_int x, y, w, z, r, p, q;
  int n, m;
  
  n = max(len(u), len(v));
 	if (u == 0 || v == 0) return 0;
  else if (n <= threshold) return u * v; // threshold는 실험적으로 결정
  else{
    m = n / 2;
    x = u / 10^m; // 이 연산은 그저 shift라 시간 복잡도에 영향 없음
    y = u % 10^m; // 여기도 마찬가지
    r = prod(x + y, w + z);
    p = prod(x, w);
    q = prod(y, z);
  }
  return p * 10^{2m} + (r - p - q)*10^m + q;
}
```

- $W(n) = 3W(n / 2) + cn$ (cn은 곱셈)
- $O(n^2)$이던 large number multiplication이 $O(n^{1.58})$까지 됨^^



- Closest Pair Problem (최근접 점의 쌍 문제)

```python
def closestPair(S, k):
  # 입력 S : n개 점들의 집합
  
  S.sort(key=lambda x: x[0])  # x좌표 오름차순 정렬
  if n <= k:
    return (k개의 점에서 closest pair)
  
  S를 같은 크기의 Sl과 Sr로 분할
  dl = closestPair(Sl, k)
  dr = closestPair(Sr, k)
  dlr = min(dl, dr)
  dlr에 의해 구성된 중간 영역에서의 closest pair dc 찾음
  
  return min(dlr, dc)
  
```

- 시간 복잡도

  - $T(n) = 2*T(n / 2) + f(n)$
  - f(n)이 $cn^2$이면, 이건 $O(n^2)$

  

# 12강

## dp

- dp

  - 작은 사이즈 instance의 optimal solution을 table에 저장해서 이걸 바탕으로 큰 사이즈의 instance에 대한 solution을 얻는 것

- Shortest Path Problem

  - 종류

    - single to single

    - single source all destination shortest path problem (다익스트라)
      - s_node에서 다른 모든 vertex들 까지의 shortest path
      - 다익스트라
        - greedy approach
        - negative cost edge 있으면 안됨.
        - Shortest path spanning tree 얻을 수 있음
    - All pairs shortest path problem (플로이드 와샬)
      - dp approach
      - negative cost edge에도 잘 작동
      - 문논, 음의 cycle 있으면 안됨.

  - 문제 유형
    - **step 1. shortest path 길이 구하기**
    - **step 2. 실제 path 구하기 (back tracing 이용)**



- **플로이드 와샬**

  - Notation

    - $D_k(i, k) \coloneqq$ i ~ j path길이 s.t only 인덱스 k 이하의 노드만 이용
    - $D_k(i, k) \coloneqq W(i,j)$ (cost edge)

  - Pseudo code

    ```cpp
    void floyd (int n, const number W[][], number D[][]) {
      D = W; // 초기화
      for (k = 1; k <= n; k++) { // 인덱스 하나씩 추가하면서
        for (i = 1; i <= n; i++) { // 모든 vertex 쌍에 대하여
          for (j = 1; j <= n; j++) {
            D[i][j] = min(D[i][j], D[i][k] + D[k][j]);
          }
        }
      }
    }
    ```

  - Time Complexity

    - $\Theta(n^3) = O(n^3)$

  - **실제 path 구하기**

    ```cpp
    D = W; // 초기화
    for (k = 1; k <= n; k++) { // 인덱스 하나씩 추가하면서
      for (i = 1; i <= n; i++) { // 모든 vertex 쌍에 대하여
        for (j = 1; j <= n; j++) {
          if (D[i][k] != MAX && D[k][j] != MAX) {
            if (D[i][k] + D[k][j] < D[i][j]) {
            D[i][j] = D[i][k] + D[k][j];
            P[i][j] = k; // k를 반드시 지난다.
          }
          }
        }
      }
    }
    ```

    ```c
    void path (int s, int e) {
      if (P[s][e] != 0) {
        path(s, P[s][e]);
        print(P[s][e]);
        path(P[s][e], e);
      }
    }
    ```

  

# 13강

- **Principle of Optimality**

  - sub instance의 optimal solution은 전체 instance의 optimal solution에 무적권 포함되어있다는 개념 (역은 not true)
  - 그니까 이 principle of optimality를 만족하는 것을 증명할 때는 아래와 같은 방법을 따른다.
    - 가정 : 큰 instance가 optimal인데, 작은 instance가 optimal이 아니라고 해보자
    - 결론 : 그러면 큰 instance가 optimal이라는 데에 모순!

- **Chained Matrix Multiplication**

  - principle of optimality 만족? =? Yes

  - 이걸 divide and conquer로 한다면?

    ```cpp
    int CMdc(i, j) {
      if (i == j) return 0;
      else if (i == j - 1) return (# of muls for AiAj);
      else {
        ans = MAX;
        for (k = i + 1; k = i + j - 1; k++) {
          ans = min(CMdc(i, k) + CMdc(k + 1, j) + m_i(k+1)j)
        }
      }
    }
    ```

    => exponential time complexity

  - Def

    - Dimension of $A_k$ = $d_{k-1}d_k$ for $k=1, 2, .., n$
    - $M[i][j]$= min num of mult needed to multiply $A_i$~$ A_j$ 단, $i < j$
    - $M[i][i] = 0$

  - Recursive Property

    - $M[i][j] = \min_{i \le k \le j-1} M[i][k] + M[k + 1][j] + ddd$
    - $M[i][j] = 0$ for $1 \le i \le j \le n$

  - Pseudo Code

    ```cpp
    int minmult(int n, const int d[], index P[][]) {
      index i, j, k, diagonal;
      int M[1..n][1..n];
      
      for (i = 1; i <= n; i++) {  // 초기화
        M[i][i] = 0;
      }
      for (diagonal = 1; diagonal <= n - 1 ; diogonal++) {
        for (i = 1; i <= n; i++) {
          j = i + diagonal;
        	M[i][j] = min_{i <= k <= j - 1} (M[i][k] + M[k + 1][j] + d[i - 1]*d[k]*d[j]);
        	P[i][j] = a value of that give the minimum;
        }
      }
    	return M[1][n];
    ```

    

  - **실제 Path 구하기**

    ```cpp
    void order (index i, index j) {
      if (i == j) {
        cout << "Ai" << i;
        return;
      }
      
      k = P[i][j];
      cout << "(";
      order(i, k);
      order(k + 1, j);
      cout << ")";
    }
    ```

  - Time complexity

    - $\Theta(n^3) = O(n^3)$

    

    

    

- **Optimal Binary Search Tree**
  - **Static Data**를 관리하는 자료구조에 대해 생각
    - 초기에 자료구조 설정해 놓고, 
    - 이후에는 only **search** operation
  - Search 빈도가 높은 key를 낮은 레벨(루트 쪽)에 배정해 두는 것이 Average Search Time을 줄인다.



# 14강

- **Optimal Binary Search Tree** (이어서)

  - Notation

    - $A[i][j]$ : **avg search time** for a binary search tree s.t $KEY_i, KEY_{i+1}, .. KEY_{j}$
    - edge case
      - $A[i]A[i-1] = 0$
      - $A[i][i] = p_i$
    - $A[i][j] = min_{i \le k \le j}(A[i][k-1]+A[k+1][j] + \Sigma_{m=i}^{j}p_m)$ 

  - Pseudo Code

    ```cpp
    void optserachtree (int n, const float p[], float& minavg, index R[][]) {
      index i, j, k, diagonal;
      float A[1..n + 1][0..n];
      
      for (i = 1; i <= n; i++) {
        A[i][i - 1] = 0;
        A[i][i] = p[i];
        R[i][i] = i;
        R[i][i - 1] = 0;
      }
      
      for (diagonal = 1; diagonal <= n - 1; diagonal++) {
        for (i = 1; i <= n - diagonal; i++) {
          j = i + diagonal;
          A[i][j] = min_{i <= k <= j} (A[i][k - 1] + A[k + 1][j]) + p_{i~j}
          R[i][j] = a value of 'k' that gave the minimum;
        }
      }
      minavg = A[1][n];
    ```

  - Time complexity

    - $\Theta(n^3) = O(n^3)$

  - **실제 BST 구하기**

    ```cpp
    node_pointer tree (intex i, j) {
      index k;
      node_pointer p;
      
      k = R[i][j];
      if (k == 0) {
        return NULL;
      }
      
      else {
        p = new nodetype;
        p -> key = Key[k];
        p -> left = tree(i, k - 1);
        p -> right = tree(k + 1, j);
        return p;
      }
    }
    ```

    => Time complexity $T(n) = \Theta(n)$

  

  

- **Traveling Salesperson Problem (TSP)**

  - 개념
    - 다른 vertex 한번씩만 찍고 다시 돌아오는 cycle (Hmiltonian cycle)
    - NP-hard 문제
  - Notation
    - $V = \{v1, v2, .., v_n\}$
    - $W[i][j] \coloneqq$ edge cost
    - $D[v_i][A] \coloneqq$ vi에서 v1으로 돌아오는 path 길이 s.t 모든 vertex가 A에 있고, 딱 한번씩만 지남
  - Recursive Property
    - $D[v_i][A] = min_{j:v_j \in A} (W[i][j] + D[v_j][A - \{v_j\}])$ if $A \neq \empty$
    - $D[v_i][\empty] = W[i][1]$
    - Length of Optimal Tour
      - $D[v_i][V - \{ v_1\}] = min_{2 \le j \le n} (W[i][j] + D[v_j][A - \{v_1, v_j\}])$

  - Pseudo Code

    ```cpp
    number D[1..n][subset of V - {v1}];
    
    // init
    for (int i = 2; i <= n; i++) {
      D[i][empty_set] = W[i][1];
    }
    
    for (k = 1; k <= n - 2; k++) {  // subset size
      for (all subsets of V - {v1} containing k vertices called A) {
        for (i s.t i != 1 and vi is not in A) {
          D[i][A] = min_{vj in A} (W[i][j] + D[j][A - {vj}];
    			P[i][A] = value of j that gave the minimum;
        }
      }
    }
    D[1][V - {v1}] = min_{2 <= j <= n} (W[1][j] + D[j][A - {v1, vj}];
    P[1][V - {v1}] = value of j that gave the minimum;
    minlength = D[1][V - {v1}];
    ```

    - Time Complexity
      - $\Theta(n^22^n)$
    - Space Complexity (size of D[] and P[])
      - $M(n) = 2n2^{n-1} = \Theta(n2^n)$
    - **실제 Path 구하기**
      - 가능



# 15강

- **냅색**
  - 개념
    - fractional 냅색 => 가성비 기준 greedy로 조지면, optimal 얻음
    - 0/1 냅색 => dp
  - Principle Optimality
    - $x_1 = a_1, .., x_n = a_n$이 optimal solution이라고 가정
    - if $a_n$ = 0
      - $a_1, .., a_{n-1}$이 optimal일 수밖에 없음. (capacity $W$ 내에서)
    - elif $a_n$ = 1
      - $a_1, .., a_{n-1}$이 optimal일 수밖에 없음. (capacity $W - w_n$ 내에서)
  - Recursive Property
    - $P[i][w] = max(P[i - 1][j], P[i-1][w-w_i] +p_i)$ 에 불과 (단, $w_i \le w$)
    - $P[n][W]$ is the maximum profit
  - 시간복잡도
    - $\Theta(nW)$



- **Edit Dsitance**
  - 3개의  operation
    - 삽입
    - 삭제
    - 대체 (substitute)
  - **편집거리 (edit distance)**
    - **S를 T로 변환시키는 데 필요한 최소의 편집 operation 연산 횟수**
  - Notation
    - $E[i, j] \coloneqq$ $S[:i]$를 $T[:j]$로 변환 시키는 데 필요한 최소 edit distance
  - Recursive Property
    - $E[i, j] = min(E[i - 1, j] + 1, E[i, j - 1] + 1, E[i, j] + \alpha)$
  - **Back Tracing**
    - 3군데에서 어디에서 왔는가를 다시 계산해서 거꾸로 올라가면 됨



# 16강

- **MIND(Maximum Independent Set) in Tree (boj 2533: 사회망 서비스)**

  - 개념

    - 일반적인  graph라면, 이 문제는  NP-hard지만 Instance에 제한을 가하면, polynomial이 될 수 있음
    - graph를 tree구조에서만 생각한다면, polynomial time 알고리즘으로 해결 가능

  - Pseudo Code

    ```cpp
    // dfs 기반
    if (v is a leaf) {
      D1(v) = 1 and D0(v) = 0
    }
    
    else {
      let chd1, chd2, .. , chdk be the children of v then,
      D1(v) = 1 + sum(D0(chdi), i = 1, 2, .., k);
      D0(v) = sum(max(D0(chdi), D1(chdi)), i = 1, 2, .., k);
    }
    ```

  - **실제  MIND 구하기**

    - binary tree라면,
      - preorder로!
        - 자신을 결정하고, children의 포함 여부를 결정
    - 일반  tree라면,
      - BFS!

    

  - 시간 복잡도
    - $\Theta(|V|)$ - linear time

  

  

- DAG (Directed Acyclic Graphs)에서  

  - AOV (Activity on Vertex) 
    - => topological ordering 알고리즘
  - **AOE (Activity on Edge)**
    - 개념
      - Time to complete the task 
        - => the cost of longest path (called **critical path**)
        - => minimum time to finish the project
      - 인스턴스를 DAG로 제한해서 longest path의 길이를 구하면, 이건 dp로 polynomial time에 가능함. (제한 안하면 NP-hard)
    - Notations
      - Variables on edge
        - early(i) : the earliest time for activity i may start
        - late(i) : the latest time that the activity may start without increasing the project duration
        - **early(i) <= activity i의 가능한 시작 시간 <= late(i)**
      - Variables on each vertices
        - $earliest[k]$ : the earliest time that event k can occur
        - $latest[k]$ : the latest time that event k may occur without increasing the project duration
    - Recursive Property
      - $k => activity~ i => l$ 인 상황에서
      - $early(i) = earliest[k]$
      - $late(i) = latest[l] - duration~of <k, l>$
      - Computing $earliest[l]$ by **forward topological searching**
        - 맨 처음 $earliest[0] = 0$으로 줌
        - $earliest[l]=max_{k \in P(l)}(earliest[k] + duration ~of <k, l>)$
      - Computing $latest[l]$ by **backward topological searching**
        - 맨 뒤에 dummy 도착 vertex를 만들어서 $latest[n + 1] = DURATION$ 줌
        - $earliest[k]=min_{l \in S(k)}(earliest[k] + duration ~of <k, l>)$
    - Remarks
      - task가 성공적으로 끝나려면, $d \ge earliest(n + 1)$
        - $earliest(n + 1)$ : 전체 일을 마칠 수 있는 최소시간
      - If $early(i) = late(i)$, we call the activity $critical$
      - $slack(i) \coloneqq late(i) - early(i)$ (느슨한 정도)
      - If a path from source to desination has edges with **zero skew**, the path is called a ***critical path***
    - 



## Greedy

-  거스름돈 문제
  - 동전의 단위에 따라서, greedy가 먹히지 않을 수도 있음
  - => 그런 경우 dp로 해야함

- MST
  - Spanning Tree
    - T = (V, E') (E'은 E의 부분집합)
    - **Minimum Spanning Tree = edge cost sum이 제일 작은 spanning tree**
  - Steiner Tree
    - S가 주어짐
      - 주어지는 S가 S = V라면, Spanning Tree인 셈
    - T = (V', E' ) (V'은 S를 cover 해야함, E'는 E의 부분집합)
    - **Minimum Steiner Tree = edge cost sum이 제일 작은 steiner tree**

- 프림

  - Pseudo Code

    ```python
    # init
    F = set()
    Y = {v1}
    
    while (the instance is not solved) {
      select a vertex in V - Y that is nearest to Y  # 여기를 잘 만들어야 함
      add vertex to Y;
      add the edge to F;
      if (Y == V) {
        the instance is solved;
      }
    }
    ```

    ```cpp
    void prim(int n, const number W[][], set_of_edges& F) {
      index i;
      index vnear;
      index nearest[2..n];
      number min;
      number distance[2..n];
      edge e;
      
      F = empty_set();
      for (i = 2; i <= n; i++) {
        nearest[i] = 1;
        distance[i] = W[1][i];
      }
      
      repeat (n - 1 times) {
        min = INF;
        for (i = 2; i <= n; i++) {
          if (0 <= distance[i] < min) {
            min = distance[i];
          	vnear = i;
          }
        }
       	c = edge connecting vnear~nearest[vnear];
        add c to F;
        distance[vnear] = -1;
        for (i = 2; i <= n; i++) {
          if 
        }
        
        
        
      }
    }
    ```

    

    

- 크루스칼

- 다익스트라

- 











