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
    ![MPU](/img/MPU.jpg)
- 메모리, 하드웨어 리소스가 제한적임
- 시스템의 보안을 위한 2가지 방향이 있음
  1. Remote Attestation
  2. Software Security

---
#### **Remote Attestation**

**기본적인 구조**   

![Basic](/img/Basic.jpg)   

    Verifier : 서버 관리자
    Prover : IoT 장비

**SMART\[NDSS'12\]**


**C-FLAT\[CCS'16\]**

---
#### **Software Security**   

**EPOXY\[S&P'17\]**   


**MINION\[NDSS'18\]**   

**CFI CaRE\[RAID'17\]**   

