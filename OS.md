# 2강

## what is OS

- OS : sw pragram that 하드웨어와 컴퓨터 user 자원을 효율적으로 interaction
  - usr view : ease of view, performance
  - sys view : resource allocation, control



## 컴퓨터 구조

- CPU와 device가 각각 비동기적으로 움직이고, 서로 bus로 소통하며, 중간 결과가 MEM에 기록되는 방식
- CPU가 도대체 언제 device의 operation이 끝나는지 알 수 있을까? => **interrupt**



## Interrupt

- HW 관점에서의 interrupt

  - IRQ - PIC - CPU

- SW 관점에서의 interrupt

  - CPU가 `interrupt vector table`을 확인함

  - | IRQ    | address |
    | ------ | ------- |
    | 0번 IRQ | 1000번지  |
    | 1번 IRQ | 2030번지  |
    | ..     | ..      |

    Interrupt Service Routine(= Interrupt Handler)



## Storage

- Main MEM 
  - RAM
  - `volatile`
- Secondary Storage
  - HDD -> seek time + rotational latency + read / write time
  - SSD
  - `non-volatile`



## 단위

- K -> M -> G -> T : 2^10씩 곱해짐



## Storage Hierarchy

- Primary Storage
  - reg
  - cache
  - main MEM
- Secondary Storage
  - non-volatile MEM
  - HDD, SSD



## Caching

- cache management
- consistency



## DMA (Direct Memory Access)

CPU에서 I/O request가 왔을 때!

- data 하나 옮기고 CPU에 interrupt 거는게 아님. 이 방식은 CPU에 부하가 심함
- device contoller가 data를 CPU 개입없이 `DMA buffer`에다가 싹 다 옮기고
- 다 옮기면 CPU에 interrupt
- 그러면 CPU가 data를 `DMA buffer`에서 줏어옴



## Multiprogramming vs Multi tasking

- Multi programming
  - multiple한 job들이 동시에 MEM에 올라 와서 수행되는 환경
  - job scheduling
- Multi tasking
  - time-sharing
  - interactive computing
  - process
  - CPU scheduling
  - swapping
  - virtual MEM : MEM에 프로그램 통째로 안 옮기고도, program 돌릴 수 있음!