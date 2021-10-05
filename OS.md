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



