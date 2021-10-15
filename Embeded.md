# 1강

- 임베디드 시스템 정의
  - dedicated function
  - OS는 있을 수도 있고, 없을 수도(`firmware` : os 없이 동작하는 sw) 있다.
- 임베디드 시스템 HW component
  - `processor` : 다양
    - micro-processor
    - micro-controller
  - `MEM` : 다양
    - volatile (power 끄면 data 사라짐)
      - DRAM
      - SRAM
    - non-volatile (power 꺼도 data 남아있음)
  - `stroage` : 이따금씩
  - `peripheral device` : 필요에 따라



# 2강

- MEM
  - volatile
    - DRAM
      - capacity에 포커스를 두고 설계
      - 20ns 이쯤
      - 전기에너지가 질질질 샌다.. -> **refresh**라는 개념
      - refresh : 주기적으로 값을 다시 읽어서 rewrite
      - non-deterministic
        - access speed가 가변적이다
        - read / write 요청이 refresh가 진행 중일때 요청하면 느려지기도 하고, DRAM안에 cache같은 구조 row buffer에 data가 있느냐 없느냐에 따라 access speed 달라짐
    - SRAM
      - speed와 안정성에 포커스를 두고 설계
      - 0.2ns ~ 3ns 이쯤
      - deterministic
        - 변수를 만들어 내는 요소가 없다.
  - non-volatile
    - 플래시 메모리
      - HDD와 달리 mechanical한 요소가 없다.
      - NAND 플래시 메모리 - 주로 한국에서
        - 커다란 용량의 storage로 사용하려고
      - NOR 플래시 메모리 - 인텔에서
        - CPU랑 연동되어서 instruction을 위한 MEM
    - STT-MRAM
      - 개빠름
      - non-volatile인데 거의 SRAM에 근접하게 빠르다
    - PCM
      - DRAM에 비견되는 speed를 가지고 있다



- I/O device
  - CPU가 I/O device와 통신하는 방법 : Polling vs Interrupt
    - polling
      - CPU가 I/O device한테 계속 물어보고 정보 가져오는거.
      - 나한테 요청할 거 있으심?
    - Interrupt
      - I/O device가 CPU한테 일을 요청하고 싶을 때, CPU를 stop시키고, 요청.
      - ~ 해줘!
  - 외부의 아날로그 정보를 sensor로 받아들일 때, AtoD, DtoA conversion
  - CPU가 I/O device와 커뮤니케이션 하는 메커니즘
    - serial port
      - 와이어 하나에다가 sequential한 신호 보냄
      - 1001101..
    - parallel port
      - 와이어 여러개
      - 칩과 칩, 칩과 디바이스를 연결하는 데에는 거의 안쓰고 있음
      - CPU 안에 블럭과 블럭을 연결하는 정도에 사용
  - USB
    - 임베디드 device를 아예 컴퓨터랑 연결하는 heavy한 데 사용(마우스, 키보드)
  - SPI, I2C
    - 간단한 센서를 연결



# 3강

- CPI = IC * CPI * CCT
- IC
  - ISA (Instruction Set architecture)
    - RISC 얘가 더 좋음
    - CISC
- Power consumption = $P_{static} + P_{dynamic}$
  - $P_{static}$ 
    - 기초대사량 같은 거
    - os조차 돌지 않는 상황에서도 생기는 전력누수
  - $P_{dynamic}$
    - CPU 돌릴 때 소모되는 power



# 4강

- $P_{dynamic}$
  - $Power_{dynamic}$ = (1 / 2) * Capacitive Load * $V^2$ * freq_switched
  - $Energy$ = CapacitiveLoad * $V^2$
  - V를 낮추는 방향(성능 감소)으로 Power를 낮추는것은 반드시 freq_switched도 낮추는 것을 유도한다.
  - (중요한 기술) Dynamic  Voltage Freq Scaling
- $P_{static}$
  - 아무것도 안하고 가만히 둬도 질질질 새면서 소모되는 Power (Leakage Current)
  - $P_{static} = Current_{static}*V$
  - (중요한 기술) Dynamic Power management
- 앎달의 법칙
  - common case를 빠르게 해야함



여기서부터 chap 3. ISA, Datapath, and Pipeline

- MIPS ISA
  - R - format 
    - Reg 3개 씀
    - add \$1, \$2, \$3
  - I - format
    - lw, sw
      - LW \$1, 100(\$2)
    - Beq
      - beq \$1, \$2, 100
        - \$1이랑 \$2 비교 해서 PC + 100 * 4 + 4로 점프

- Hazards

  - `Structural Hazards`
    - 하드웨어 메모리가 하나뿐이어서 instruction fetch랑 mem access랑 동시에 겹쳐버리는 문제
    - inst 메모리와 data 메모리를 분리하면 그만
  - `Data Hazards`

  - `Control Hazards`

    - 무릇 branch란

      1. 브랜치 할 지 말 지 (Branch outcome resolution)
      2. 어떤 addr로 브랜치 할 지 (Branch Target Addr resolution)

      이 2가지를 결정해야 함



# 5강

- `Data Hazards`

  - `RAW` - true dependency

  - `WAR` - anti dependency

  - `WAW` - output dependency

    => RAW 는 어떻게든 forwarding, 그래도 bubble 생기면 rescheduling

    => 아래 2개는 inst 순서 바꿔서 reschedule을 하면 문제가 될 수 있음.

- `Control Hazards`

  해결1. 가만냅두자

  해결2. Prediction (branch 안 일어날 것으로 가정)

  해결3. Prediction (branch 일어나는 것으로 가정)

  해결4. Delay slot : `"무적권 수행할 명령어"`를 위치시킬 수 있는 공간 (젤 됴호음)

   - 이 전 명령 중 독립적인거 가져옴.

   - branch target 땡겨옴.

   - branch 안 일어날거라 생각하고 다음 명령 땡겨옴.

     해결3과 해결4의 차이 : 해결3은 정책하나를 정하는거고 해결4는 컴파일러가 보고 적절한 거를 잘 선택해서 가져오는 것인듯



# 6강

- Instruction Level Parallelism
  - 좀 더 발전해서 요새는 dynamic approach를 시도 
  - <-> static approach :  컴파일러가 프로그램 run 전에 여러가지를 판단
- Loop Level Parallelism
  - dynamic via branch prediction
  - static via loop unrolling by compiler



# 7강

```c
for (i = 1000; i > 0; i = i - 1){
  	x[i] = x[i] + s;
}
```

를 무지성으로 complie하면, 하나의 loop에 stall이 5개나 생김.



- 먼저, `loop overhead`를 개선해볼 수 있음. -> Branch hazard의 빈도수를 줄여버림
  - `Loop unrolling` 조져벌힘
  - 필연적으로 `register renaming`을 수반함
  - 4배 펼치면, loop overhead가 1/4배로 줄어듦

  

- (코드의 종속성을 잘 판단해야겠지만, 할 수만 있다면) `rescheduling` 까지 조져벌힘 -> `Control Hazard`까지 제거할 수 있음
  - iteration당 9 사이클을 3.5 사이클까지 줄여벌임 ㄷ



- 3가지 한계
  - 욕심부려서 더 펼치면 좋아지기야 하겠지만은 개선 효과가 점점 떨어짐
  - 코드 사이즈가 커짐
  - 레지스터 모자르게 됨 (Register Pressure)



이제 chap 4b. Instruction Level Parallelism 2

Static Branch Prediction에서 제일 뭐 노력해봐야 `Trace(profile)-based branch prediction`.

특정 주소에 있는 branch가 take를 많이 하더라 이런 통계를 갖고 prediction 하는거.



# 8강







