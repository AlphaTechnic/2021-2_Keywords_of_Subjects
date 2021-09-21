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







