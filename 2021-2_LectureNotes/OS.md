# 2강

- OS의 정의

  - OS : sw pragram that 하드웨어와 컴퓨터 user 자원을 효율적으로 interaction
    - `usr view` : program for ease of view and performance
    - `sys view` : program for resource allocation, control



- 컴퓨터 구조

  - CPU와 device가 각각 비동기적으로 움직이고, 서로 bus로 소통하며, 중간 결과가 MEM에 기록되는 방식
  - CPU가 도대체 언제 device의 operation이 끝나는지 알 수 있을까? => **interrupt**



- `Interrupt`

  - HW 관점에서의 interrupt

    - IRQ - PIC - CPU 
    - IRQs are mapped by PIC to generate interrupts to CPU
      - IRQ 몇 번이 발생했습니다!

  - SW 관점에서의 interrupt

    - CPU가 `interrupt vector table`을 확인함

    - | IRQ    | address |
      | ------ | ------- |
      | 0번 IRQ | 1000번지  |
      | 1번 IRQ | 2030번지  |
      | ..     | ..      |

      위의 주소로 점프하면, service routine으로 점프하는 것
      
    - Interrupt Service Routine(= ISR = Interrupt Handler)

  

- Storage

  - Main MEM 
    - RAM
    - `volatile`
  - Secondary Storage
    - HDD -> seek time + rotational latency + read / write time
    - SSD
    - `non-volatile`



- 단위

  - K -> M -> G -> T : 2^10씩 곱해짐



- Storage Hierarchy

  - Primary Storage
    - reg
    - cache
    - main MEM
  - Secondary Storage
    - non-volatile MEM
    - HDD, SSD



- Caching

  - cache management
  - consistency



- `DMA (Direct Memory Access)`

  CPU에서 device로 I/O request가 왔을 때!

  - data 하나 메모리에 옮기고 CPU에 interrupt 거는게 아님. 이 방식은 CPU에 부하가 심함
  - device contoller가 data를 CPU 개입없이 `DMA buffer`에다가 싹 다 옮기고
  - 다 옮기면 CPU에 interrupt
  - 그러면 CPU가 data를 `DMA buffer`에서 줏어옴



- Multiprogramming vs Multi tasking

  - Multi programming
    - multiple한 job들이 동시에 MEM에 올라 와서 수행되는 환경
    - job scheduling
  - Multi tasking
    - time-sharing
    - interactive computing
    - process
    - CPU scheduling
    - swapping
    - `virtual MEM` : MEM에 프로그램 통째로 안 옮기고도, program 돌릴 수 있음!
  - Multi 프로그래밍은 CPU가 쉬지 않게 하는 방법
  - Multi 태스킹은 마치 동시에 여러 프로그램이 돌아가는 것처럼 illusion을 주는 방법



# 3강

- OS operation for **Protectoin** (incorrect, malicious 접근에 대한)
  - Dualmode operation
    - 모드가 2개 (usr mode, kernel mode)
  - I/O protection
    - 오직 sys call 만으로 IO를 제어하도록
  - MEM
    1. Interrupt vector, Interrupt Service Routine(ISR) 아무나 못바꾸게!
    2. base + limit 개념으로 프로그램마다 독자적인 메모리 영역을 쓰게 함
  - Timer
    - 타이머가 항상 돌면서 주기적으로 timer에 대한 interrupt를 발생시킴
      - ex ) time sharing



- **OS services and SystemCalls**
  - C프로그램이 라이브러리를 통해 sys call을 부르면, (이를테면 read())
  - `interrupt vector table`로 간 다음에 (사용자가 라이브러리로 interrupt를 걸었어 -> x80위치로)
  - `system call table`로 감 (read service야)
- System Call parameter passing
  - param을 reg에 직접 넣음
  - param을 MEM에 넣고 주소를 reg에
  - Stack에 주고 pop pop 해서 사용



- System Boot
  - Power on! 하면 `Boot Loader`가 운영체제 로딩해서 수행시킴 -> 2 step
  - 1 step - **ROM**에 있는 코드 실행
    - **POST**(Power On Self Test)
      - device에 문제 없는지 chk
    - Boot device Selection
      - 부팅 디스크 HDD로? SSD로? usb로? CDROM으로? 네트워크로?
  - 2 step - **MBR**(Master Boot Record)에 있는 코드 실행
    - read MBR of Boot Device and -> 실행
      - MBR에 적힌 코드가 하는 일 
        - 어떤 운영체제가 부팅을 할지를 결정 
        - 그 운영체제가 돌아가기 위한 기본적인 셋팅, 초기화



- OS Structure
  - **monotholic**한 구조 (큰 한 덩어리)
    - ex ) UNIX
  - **micro-kernel** (OS를 아주 작게 만들어놓고 웬만한건 usr space에 밀어 넣음)
    - ex ) MAC OS, 안드로이드
    - 커널 아키텍쳐 이식은 편함
    - secure 좋음 (커널 털리면 다 털리는건데 그게 사이즈가 작으니)
    - usr space, kernel space 왔다갔다해야되서 속도에서 손해



# 4강

- **Virtual Machine**

  - 정의 : abstract hw that 여러 개의 기계를 돌리는 것처럼 illusion을 주는

  - 이점

    - 운영체제 복제도 가능
    - (이를테면, 서버 컴퓨터) CPU Utilization을 극대화

  - 환경의 종류

    - Navive VM

      - virtual machine monitor(VMM)를 bare machine 바로 위에 올림

    - Hosted VM

      - hw위에 -> host OS 위에 -> 올림

        

**end of ch2 : System Structure**

**start of ch3 : Process**



- Procss (= Job = Task)
  -  정의
    - `정의` : Program in execution
    - `Program`은 Disk에 있는 binary file일 뿐
  - 구성
    - `stack` - local variables
    - `heap` - dynamic allocation
    - `data` - global var
    - `code` - 어셈블리 명령어들



- Process State
  - `new`
  - `ready` (new에서 메모리에 올라가면 = admitted)
  - `running`
  - `waiting`
  - `terminated`

- **PCB**(Process Control Block) - 프로세스 관리하는 자료구조
  - process 의 context들(pid, state, program counter, mem limits, ..)이 저장되어 있다.



- Process Scheduling
  - `I/O bound process`
  - `CPU bound process`
  - I/O bound process를 잔뜩 MEM에 올려놓는 것은 CPU utilization을 극대화하는 방향이 아님
- Scheduling Queues
  - PCB1 - PCB2 - .. PCB10
  - `Ready Queue` : 레디상태의 PCB들 줄줄이..
  - `I/O Wait Queue` (= `Device Queue`) : wait 상태의 PCB들이 줄줄이..
- **Scheduler**
  - Queue의 Process들을 순서대로 돌려가면서 수행하는 기능 외에
  - (프로세스를 위한 메모리 공간 모자라다면) Process를 골라서 외부(디스크)로 뱉어낼 수도 있다. (`swap out`)
- Context Switch
  - `Context` : PCB에 들어있는 프로세스와 관련된 정보
  - 기본적으로 오버헤드임



# 5강

- Operations : Process **Creation** in Unix
  - `fork()`

  - `chd process`는 consists of **a cpy of the addr space** of the `par process`

  - `exec()`

    - chd의 code 공간을 싹 지우고, new program 실행

    - 이를테면, main()에서 수행한 fork()는 code 공간에 main의 내용이 써져 있다가, `execlp("/bin/ls", "ls", NULL)`을 수행하면서 main의 내용을 지우고, ls의 내용을 적는다.

      ![process creation](./imgs_for_docs/fork.png)

      

- Operations : Process **Termination** in Unix

  - `reparent` 정책을 쓰고 있음.
    - 부모 죽으면 자식 뭉탱이들 연쇄적으로 다 죽는 `cascading termination` 정책도 있긴함.

  

- `Zombie` vs `Orphan`
  - zombie
    - 자식 exit() 했는데, 부모가 wait(&status)로 자식의 종료를 받아주질 아니함
  - orphan
    - 자식이 실행 중인데 부모가 먼저 죽어버림



- Address Space
  - process1과 process2가 각각 독립된 code, data, heap, stack의 4GB 공간을 갖는것처럼 생각해도 되게끔 함. (physical한 개념은 아니고, logical, virtual의 개념)
  - 그럼 실제 physical하게는 어떻게 관리되고 있느냐
  - process에 사용되는 메모리공간이 `page` 단위로 잘개 쪼개져서 `frame` 형태로 `physical` 메모리에 올라가 있음.
    - => 실제 4GB가 없어도 됨.



# 6강

- Cooperating Process

- **IPC**(Inter Process Communication)

  - `방식1` : **msg passing**
    - 3가지 이슈 : Naming, Synchronization, Buffering
    - `Naming` : 
      - direct 
      - indirect : 중간에 mailbox를 두고 소통
    - `Synchronization` : Blocking < - > Asynch, Non-blocking 
    - `Buffering`
      - zero capacity : sender가 recv 올 때까지 기다려야 함. (**랑데뷰**)
      - bdd capacity :  buffer가 full인 경우 sender가 기다림
  - `방식2` : **shared MEM**

  

  

# 7강

- IPC in Unix:
  - 전통적인 IPCs : signal, **pipe**, socket
  - System V IPCs : msg queue, semaphore, shared MEM



- Pipe
  - **unidirectional**
    1. Ordinary(anonymous) Pipe
       - par - chd 사이에서만 쓸 수 있는 IPC 방법
       - writer는 `write(fd[1]);`
       - reader는 `read(fd[0]);`
    2. Named Pipe
       - par - chd 뿐만 아니라 어떤 Process끼리도 IPC하는 방법
       - 특정 경로에 파일 만들어 쓰고, 그거 읽어오는 것에 불과

- Communication in Client-Server Systems
  - Pipe가 동일 기계 내에서 통신이라면, 이건 떨어진 기계끼리(도) 통신
    1. **Socket**
       - endpoint of communication (=IP addr + port #)
    2. **Remote Procedure Calls**(`RPC`)
       - add function, mul function 같은 것을 remote에서 부르는 것
       - client는 (add관련, mul관련) client stub을 만들고, server는 server stub을 만들어서, client가 링크할 때 코드가 들어가도록 작업
       - 그 사이의 연결은 문논 Network가



// 이제 새로운 chapter 4. Thread and Concurrency

- Motivation (Overhead in Process Model)
  - Concurrent 프로그래밍이 유용한 것은 자명
  - Process에서 context switch가 있으려면, P1의 정보를 save하고, P2를 restore하는 것인데 여기서 오버헤드가 크다.
  - Process creation 같은 경우도 싹다 카피하기 땜에 heavy하다.
  - 오버헤드를 적게 하면서, concurrency를 유지할 수 없을까?
- Thread란?
  - subprocess라고 보면 됨.
  - **share** `code`, `addr space`
- Thread를 쓰면 왜 좋나?
  1. Parallelism을 얻습니다.
     - parallelism은 pysical하게 동시에
     - CPU(core)를 thread마다 여러 개 들이댈 수 있다.
  2. Concurrency를 얻습니다.
     - 이거는 illusion
     - I/O bound 작업 하는 동안 다른 thread로 스위치해서 작업
     - I/O랑 computation을 오버랩하면서 speed up 달성!
     - 특히, Server Programmin에서 I/O를 상당히 많이 해서, thread의 이득을 잔뜩 누려보릴 수 있음



# 8강

- Why Multithreaded Server?

  - multithreaded의 장점을 숫자로 보여주는 파트

  - I/O의 일을 많이 하고 있음

    

  - 예시 : 2ms for processing, 8ms for IO delay

  - T 하나라면, 2-8-2-8-.. 하나의 수행단위를 10ms에 처리, 1초(=1000ms)동안이라면 100개 처리. 즉, 100req/sec

  - T 2개라면, T1의 8ms와 T2의 2ms를 겹쳐보릴 수 있음. 즉, 125req/sec

  - hit ratio = 75%를 가정하면, avg io time = 0.75*0 + 0.25\*8ms = 2ms로 가정할 수 있음.

    - 이래버리면, 하나의 단위 수행을 2ms에 처리하게 됨. 무려, 500req/sec



- User-level Thread vs Kernel-level Thread

  - `multithreaded kernel` 

    - thread를 알 고 있는 kernel

  - User-level Thread와 Kernel-level Thread를 **매핑**하는 라이브러리? 

    - => `Kernel-level-thread-library`

    - 라이브러리를 k-level, usr-level 나누는 기준은 **매핑 여부**

    - `Kernel-level-thread-library`가 매핑을 하는 방법

      - N:1

        - usr level thread들 N개를 kernel lv thread 1개가 담당하겠다는 얘기
        - 매핑을 아니 하는 것과 동일
        - I/O할 때 block을 건다.
        - read()를 nonblock으로 짜든지 해야(`ioctl()`) data가 다 들어오지 않아도 쓰레드를 빠져나올 수 있다.
        - concurrency, parallel 입장에서, N:1은 parallelism을 얻기 힘들다
        - cannot fully utilize multicores

      - 1:1 (일반적)

        - usr level thread들 1개당 kernel lv thread 1개가 담당하겠다는 얘기
        - block problem 없음
        - Window, Linux
        - Concurrency, Parallelism 달성

      - M:N

        - usr level thread들 M개를 kernel lv thread N개가 담당하겠다는 얘기
        - Concurrency, Parallelism 달성

        

  - `User-level-thread-library`

    - 커널쓰레드와 매핑 안함
    - 모든 user thead들을 user space에서 처리
    - nonmultithreaded kernel에서 사용하게 됨
    - 정리하자면,
      - `Kernel-level-thread-library`가 N:1 모델을 택하는거? on multithreaded kernel에서 해봤자
      - $\approx$ `User-level-thread-library`가 on non-multithreaded kernel에서 하는거
      - $\approx$ `User-level-thread-library`가 on multithreaded kernel에서 하는거
      - 위의 경우들 전부, blocking문제 있고, multi CPU 이용 못함



# 9강

- Thread Issues
  - Semantics of `fork()` and `exec()` system calls
    - `exec()`을 할거라면, thread 하나만 cpy하고, `exec()`을 부르는게 효율적
    - `exec()`을 안할거면, 모든 thread를 cpy하는게 효율적
    - 따라서, UNIX는 thread에서 fork()시 그 방식을 선택할 수 있게 하는 옵션이 있음
  - Signal handling
    - Synchronous signal
      - 이를테면, thread 스스로 kill
      - 0으로 나눴다거나, 포인터 잘못 써서 seg fault
    - Asynchronous signal
      - 이를테면, `ctrl + c`
  - Thread cancellation
    - `Asynchronous cancellation`
      - 바로 쥬금
    - `Defered cancellation`
      - kill 당해도 탈이 없을 때까지 기다렸다가 쥬금
      - 안전하게 죽을 수 있는 장치라고 보면됨
      - `pthread_testcancel()`
  - Thread pools
    - req 올 때, thread creation 하는 게 아니라, 미리 n개의 thread를 생성해 놓고 대기시켜놨다가 서비스하는 방식
    - 서비스 제공 빠름
  - Thread Local Storage (`TLS`)
    - 해당 thread 내에서만 글로벌인 변수 storage
    - 다른 thread에 영향을 주지 않는다
    - `TLS sum;` 이런 느낌으루



// 이제 새로운 chap5. CPU scheduling

- I/O bound process가 많다. -> I/O bound process를 잘 돌릴 수 있는 방향으로 알고리즘을 설계해야한다.

- `CPU scheduler`

  **하는 일1.** 메모리에(ready queue에) 있는 process 중 하나를 골라 => algorithm (pick)

  **하는 일2.** CPU에 위에서 pick한 process를 할당하는 거 => dispatch 

- CPU scheduling decision![process_life_cycle](./imgs_for_docs/process_life_cycle.jpg)
    - only **dispatch** and **exit** => `non-preemptive` or `cooperate`
    - other => `preemtive`(선점형)

- **Dispatcher**

  - context switch
  - dispatch latency : 피할 수 없는 오버헤드..

- **Scheduling Criteria**

  - CPU마다 목적이 다를 수 있다.
  - wait time을 줄이겠다든가, response time을 줄이겠다든가

  1. CPU utilization
  2. Throughput
  3. Turnaround time(반환 시간) = Completion Time - Arrival Time(레디큐진입)
     - Process 쪼개지 않는 것이 turnaround time을 빠르게 하는 방향
  4. waiting time
  5. response time = FirstRun Time - Arrival Time(레디큐진입)
     - 첫번째 수행이 시작되는 시간
     - output이 나오는 시각까지가 아님. 그거는 turnaround time



- Scheduling
  1. First Come, First Sended(FCFS) scheduling
  2. Shortest-Job-First(SJF) scheduling
  3. Priority Scheduling
  4. Round-Robin(RR) scheduling
  5. Multilevel Queue Scheduling
  6. Multilevel Feedback Queue Scheduling

- 알고리즘 성능 평가
  - `input` : process state table
  - `output` : Goutt Chart

- **FCFS**

  - 선착순

  - 레디큐의 앞쪽부터 순차적으로 수행

  - non-preemptive

  - 단점

    - avg wating time 길어짐
    - time sharing system에서 문제가 됨
      - timesharing system은 response time이 짧기를 원하는 것.

    - `Convoy effect`
      - CPU burst의 길이가 긴 돼지같은 놈이 앞에서 자리차지하고 있는 문제
    - lower CPU utilization (lower device utilization)
    - 그러면, 짧은걸 먼저 돌리면 되지 않을까..?

- **SJF** scheduling

  - min avg waiting time을 주는 optimal한 알고리즘이다.
  - 그러나, CPU시간이 짧다는 것을 알아낼 수 없는게 문제..
    - 이 전에 나왔던 CPU burst의 길이를 이용해 예측(estimation)
    - 정책 중 하나로 exponential averaging
      - $\uptau_{n+1} = \alpha t_n + (1- \alpha) \uptau_n$
      - 가장 최근의 CPU burst의 길이에 비중을 많이 주는 방식

  1. Non-preemptive한 방식
  2. Preemptive한 방식
     - 신입이 더 short면 교체
     - process arrival time에 평가를 하는 것
     - Shortest Remaining Time first



# 10강

- **Priority Scheduling**
  - 여기도 non-preemptive, preeptive 2가지 종류가 있음
  - 앞서 배운 SJF도 Priority scheduling의 일부
  - 단점
    - starvation
    - 우선순위 낮아버리면 계속 뒤로 밀려서 수행 못시키고 굶어 쥬금
  - 해결
    - aging
    - 오래 기다릴수록 우선순위를 올려줌
- **Round Robin(RR) scheduling**
  - process가 각자 제한된 CPU time을 할당 받음 (= time quantum = q)
    - q가 줘헌네 크다면 사실상 FCFS
    - q가 줘헛네 작다면 사실상, 1/n 스피드로 다 동시에 돌려버리는 셈 (= **processor shring**)
  - 장점
    - **response time**이 good
  - 단점
    - turnaround time이 SJF에 비해 커질 수 있음
    - q가 줘헌네 커져서 FCFS랑 같아지면 turnaround time은 작아지지만,
    - q를 조금씩 올릴 수록, turnaround time이 점점 비례해서 줄어든다는 틀린말
      - 80%의 process가 time quantum 안에 해결되는 딱 그정도로 time quantum을 잡아준다면, 효율적이더라하는 연구가 있음
- **Multi level Queue**
  - Queue를 여러 개 둬서, 각 queue에 서로 다른 scheduling 알고리즘을 적용함
  - 예를 들어, fg는 RR로, bg는 FCFS로 이런식으루
  - Scheduling Between Queues
    - `Fixed priority scheduling`
      - starvation 가능성
    - `Time slice`
      - CPU가 80%는 queue1에 있고, 20%는 queue2에 있고 하는 정책
  - 단점
    - 프로세스가 queue1에서 queue2로 이동한다거나 못함 
    - 그걸 할 수 있게 해준게?
- **Multi level feedback Queue (MLFQ)**
  - 프로세스들이 거주지 queue를 바꿀 수가 있음
  - 언제 높은 priority의 queue로 넘기는 지, 프로세스를 맨 처음에 어떤 queue에 넣을지 같은 정책을 정해야



- **Multi - Processor scheduling**
  - Asymmetric multiporcessor
    - core 한 놈은 다른 core에게로 분배하는 기능을 맡는다거나 하는 식으로 모든 core의 기능이 동일하지 않은 것
  - **Symmetric multiporcessor (SMP)**
    - common ready queue
    - **priviate ready queue**
      - 로드 밸런싱 이슈가 있음. 특정 core만 일을 많이하고, 다른 core는 놀고 있다거나 하는 문제
      - Load Balancing
        - Migration
          - `Push migration`
            - 특정 core에서 특정한 task가 돌면서, 주기적으로 ready queue를 살펴봄.
            - 놀고 있는 core가 있으면, 그짝으루 process를 push
          - `Pull migration`
            - 각자의 core가 스스로를 되돌아보면서, 본인이 놀고있으면 로드가 많이 걸린 core에서 process를 뺏어옴
        - **Affinity**
          - 프로세스가 막 함부로 core를 옮겨다니면, cache를 못하게 됨.
          - process가 creation 되면서 affinity(유착관계) 지정 가능 (나는 core 옮기지 말아라)
            - `soft affinity`
            - `hard affinity` (절대 migration 하지 말아라)



# 11강

- **Simultaneous MultiThreading (SMT)**
  - Multicore 환경에서 Memory Stall 문제가 있음
    - processor cache miss되면, IO에 시간을 엄청 많이 쓰게됨
    - core에서 thread를 띄워서 오버랩 조져벌힘
    - computation 스위치는 HW가 지원하는 것



// 이제 ch 6, 7. Synchronization Tools and examples

- Producer and Consummer => interleaving 가능성
  - interleaving을 막는 것 = atomic하게 하는 것 = synchronization



- CS(Critical Section)

  - Race condition이 발생하여 문제가 생길 수 있는 구간
  - 안전한 CS 수행을 위한 노력
    1. Software-based approaches
    2. `TestAndSet`, `Swap`
    3. **Semaphore**
    4. language가 제공하는 synchronization이용 ex> `monitor`

  

- CS Implementation properties
  - 안전한 CS Implementation이라면 아래 3가지 property를 만족해야 함
    1. **Mutual Exclusion**
       - P0가 CS를 수행하고 있으면 P1은 CS를 수행하면 아니됨
    2. **Progress**
       - 다른 Process가 CS에 있지 않으면? 무적권 들어갈 수 있어야.
       - 즉, '다른 P가 CS에 있어서' 라는 것이 특정 P가 CS에 진입하지 못하는 유일한 이유여야함
    3. **Bdd waiting**
       - 기다리는데에는 반드시 한계가 있어야 함
       - 그러기 위해서 다른 P의 진입 횟수 제한 #가 설정되어 있어야 함



- **안전한 CS 수행을 위한 노력1. software-based approaches**

  > general structure of Pi

  ```c
  do {
    entry section
      CS
    exit section
      RS
  } while(1);
  ```

  - algorithm1

    ```c
    do {
      while (turn != i);
      CS
      turn = j;
      RS
    } while(1);
    ```

    - 반드시 strict alternation이 되어야 한다는 문제. 
    - P0가 연속으로 2번 CS에 진입한다거나 그런게 안됨. 
    - 반드시 핑퐁해야됨

  - algorithm2

    ```c
    do {
      flag[i] = true;
      while (flag[j]);
      CS
      flag[i] = false;
      RS
    } while(1);
    ```

    - P0, P1 둘 다 '나 들어갈게'가 되버리면, 데드락 걸림;;

  - Peterson's algorithm

    ```c
    do {
      flag[i] = true; turn = j;
      while (flag[j] && turn == j);
      CS
      flag[i] = false;
      RS
    } while(1);
    ```

    - algo1, algo2의 문제를 해결하여서 모든 CS property를 만조꾸함. BUT
    - modern computer에서는 compiler가 최적화를 위해 코드 순서를 뒤바꾸기 땜에 먹히지 안흠



# 12강

- **안전한 CS 수행을 위한 노력2. HW instruction으로 synchronization**

  1. disable interrupts -> 오버헤드 너무 큼

  2. atomic instruction 제공

     > `boolean TestAndSet(boolean *target)`

     ```c
     boolean TestAndSet(boolean *target) {
       boolean rv = *target;
       *target = TRUE;
       return rv;
     }
     
     // lock을 걸고(TRUE) CS에 진입하는 것에 불과
     // bdd waiting을 만족하지 못함. 특정한 P만 계속 도는게 가능
     do {
       while (TestAndSet(&lock));
       CS
       lock = FALSE;
       RS
     } while(TRUE);
     ```

     

     > `void Swap(boolean *a, boolean *b)`

     ```c
     void Swap(boolean *a, boolean *b) {
       boolean temp = *a;
       *a = *b;
       *b = temp;
     }
     
     // 역시 lock을 걸고(TRUE) CS에 진입하는 것에 불과
     // 역시 bdd waiting을 만족하지 못함. 특정한 P만 계속 도는거 가능
     do {
       while (key == TRUE) Swap(&lock, &key));
       CS
       lock = FALSE;
       RS
     } while(TRUE);
     ```

     

- **안전한 CS 수행을 위한 노력3. Semaphore**

  - Semaphore : integer 변수임 s.t 오직 P와 V로만 접근할 수 있는

    ```c
    void wait(S) { // P(S)
      while (S <= 0) do no-op;
      
      S--;
    }
    
    void signal(S) { // V(S)
      S++;
    }
    ```

  - Counting semaphore(S >= 0) vs Binary Semaphore(=mutex lock) (S == 0 or S == 1)

  - Spinlock(=busy waiting)이 이로울 때가 있는데, 세마포는 busy waiting 안함

  - Using semaphore

    ```c
    // 역시 bdd waiting은 만족하지 않고 있다.
    semaphore mutex;
    
    do {
      wait(mutex); // wait은 하나 내리는거
      CS
      signal(mutex); // signal은 하나 올리는거
      RS
    } while(1);
    ```

  - Deadlock이나 Starvation의 위험성 있음



- **안전한 CS 수행을 위한 노력4. Monitor**

  - monitor 안에서 수행하는 함수는 오직 하나임을 개런티 해줌

  - `condition variable`

    - condition을 만족하지 못해서 함수 수행을 하지 못하고 기다려야 한다면, x varialbe에 링크드리스트처럼 대기시켜놓음

    - `x.wait()` `x.signal()`

    - **세마포와 다른 점??**

      - x.signal()은 단 하나의 suspended process만 깨움
      - suspended process가 없다면, x.signal() 아무런 effect 없음

      

    - 그런데, x.signal() 하는 순간 suspended된 process가 동작하면서 monitor에 2가지 process가 돌게 됨.

    - 이걸 해결하는 정책

      - signal and wait method (Hoare's semantic)

        - signal을 주고 깨운 다음에 본인은 나가서 wait
        - 지금 signal을 주게 된게, 지금 하필 이 시점에 이 condition이 만족이 된건데, 바로 수행을 시켜줘야하지 않겠느냐는 입장

      - signal and continue method (Brinch Hansen's semantic)

        - signal을 주고 깨운 다음에 본인 수행을 이어 continue하고, 그 다음 대기타던 놈 수행

        - 위에 저놈은 context switching이 너무 많이 일어나는거 아니냐

        - 대신 위와같은 문제는 

          ```c
           // if (!condition) x.wait()  <-버려:
          while (!condition) x.wait()
          ```

          와 같은 방식으로 condition rechecking을 통해 해결함.

        - Pthread가 위와같은 방식



# 13강

- Classical Problem of synchronization

  - bdd Buffer Problem

    ```c
    semaphore full = 0;
    semaphore empty = n;
    semaphore mutex = 1;
    
    // Producer Process
    do {
      produce an item in nextp
        
      wait(empty);
      wait(mutex);
      
      add nextp to buffer
        
      signal(mutex);
      signal(full);
    } while(1);
    
    
    // Consumer Process
    do {
      wait(full);
      wait(mutex);
      
    	remove an item from buffer
        
      signal(mutex);
      signal(empty);
      
      consume the item in nextc
    } while(1);
    ```

    

  - Readers-Writers Problem

    ```c
    semaphore mutex = 1;
    semaphore wrt = 1;
    int readcount = 0;
    
    // 1st readers-writers : reader 친화적. reader는 기다리지 말아라
    // Writer Process
    do {
      wait(wrt);
      
      writing is performed
        
      signal(wrt);
    } while(1);
    
    
    // Reader Process
    do {
      wait(mutex);
      readcount++;
      if (readcount == 1) wait(wrt);
      signal(mutex);
      
     	reading is performed
      
      wait(mutex);
      readcount--;
      if (readcount == 0) signal(wrt);
      signal(mutex);
    } while(1);
    ```

    

  - Dining-Philosophers using Semaphore

    ```c
    Philosopher i;
    do {
      wait(chopstick[i]);
      wait(chopstick[(i + 1) % 5]);
      
      eat;
      
      signal(chopstick[i]);
      signal(chopstick[(i + 1) % 5]);
      
      think;
    } while(1);
    ```

    위 코드는 데드락 가능성이 있음. 전부 오른쪽 젓가락 집으려고 하면..

    적당히 정책을 쓴다해도, starvation이 생길 수 있음

    

  - Dining-Philosophers using Monitor

    ```c
    monitor dp{
      enum {thinking, hungry, eating} state[5];
     	condition self[5];
      
      void pickup(int i){
        state[i] = hungry;
        test(i);
        if (state[i] != eating) self[i].wait();
      }
      void putdown(int i){
        state[i] = thinking;
        test((i + 4) % 5);  // test left neighbor
        test((i + 1) % 5);  // test right neighbor
      }
      void test(int i){
        if ((state[(i + 4) % 5] != eating) && (state[i] == hungry) && state[(i + 1) % 5] != eating)) {
          state[i] = eating;
          self[i].signal();
        }
      }
      void init(){
        for (int i = 0; i < 5; i++)
          state[i] = thinking;
      }
      
    }
    ```

    
