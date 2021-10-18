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

> `DBL structure`

```cpp
typedef struct _DBL{
  int d;
  struct _DBL *twin;  // 다른 위치에 있는 나 자신을 가리키는 pointer
  struct _DBL *lp, *rp;
}
```

> Class for DBL pool

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



