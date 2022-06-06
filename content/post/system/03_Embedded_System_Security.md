---
title: "03 Embedded System Security"
date: 2021-05-26T02:07:23+09:00
author : "Kim Minjae"
description : "Guide to emoji usage in Hugo"
tags : [
    "system",
    "security",
    "hardware",
    "Embedded",
]
series : ["system security"]
---

#### **Embedded 시스템 개요**   
임베디드 시스템 특징
- 임베디드 시스템은 MMU를 가지고 있지 않음
  1. virtual memory를 사용하지 않음
  2. 각 디바이스에 따른 전용 메핑을 사용함
  3. MPU 레지스터들은 PPB에 있음
      -  Private Peripheral Bus:내부와 외부의 프로세서의 접근을 제공하는 메모리 영역
      -  8,12,16 개의 regions(영역)을 제공함
      -  Base & size 에따른 permission이 다름   
    ![MPU](https://gamjagoon.github.io/asdf/img/MPU.jpg)
- 메모리, 하드웨어 리소스가 제한적임
- 시스템의 보안을 위한 2가지 방향이 있음
  1. Remote Attestation
  2. Software Security

---
#### **Remote Attestation**

**기본적인 구조**   

![Basic](https://gamjagoon.github.io/asdf/img/Basic.jpg)   

    Verifier : 서버 관리자  
    Prover : IoT 장비

**SMART\[NDSS'12\]**   
- remote attestation을 지원하는 작은 하드뤠어를 사용함   
1. 작동시작시 code integrity를 확인함(무결성 검증)
2. code의 attest와 protected key를 rom으로 부터 읽어옴
3. 디바이스의 memory HMAC을 protected key를 사용하여 검증함
4. 디바이스가 정상 동작함

- memory access control을 필요로함
- 각 연산을 지원해야함

**C-FLAT\[CCS'16\]**   
- Secure World를 이용한 코드의 무결성 검증
---
#### **Software Security**   

**EPOXY\[S&P'17\]**   


**MINION\[NDSS'18\]**   
- process memory, kernel memory isolation을 사용하지 않음
- Key ideas
  - 물리적인 메모리 공간을 per-process 하여 memory views 분석함
  - memory views 를 사용하여 access control rules 을 사용함
  - unprivilaged 모드에서 동일한 프로그램을 실행함
  - View Switcher를 privileged 모드에서 실행하여 view들의 실행을 확인함    
  
**CFI CaRE\[RAID'17\]**   
- shadow stack 을 사용항 Control Flow Integrity 확보

