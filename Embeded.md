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
- $P_{static}$
  - 
