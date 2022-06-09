---
title: "02 system security : Arm trust zone"
date: 2021-05-25T00:11:34+09:00
author : "Kim Minjae"
description : "x86 Intel SGX description"
tags : [
    "system",
    "security",
    "hardware",
    "arm"
]
series : ["system security"]
---

#### **Trusted Execution Environment**   
- 고립된 실행 환경과, 안전한 실행환경을 제공함
- Trusted한 실행환경은 코드와 데이터에 대한 기밀성과 무결성을 제공하는걸 목표로함
  - Trusted Execution Environment(TEE)
  - Rich Execution Environment(REE)

#### **ARM TrustZone**   
- 인터넷에서 Digital Rights Management(DRM)을 보드에 적용한 개념
- 기본 개념은 시스템을 2개의 공간으로 분리함   
![](https://gamjagoon.github.io/img/Trust01.jpg)
- 각공간은 독립된 메모리 공간을 가지고 있음
- Peripheral devices
  - Screen
  - Touch input
- Registers
  - General-purpose
  - Special registers

#### **Exception Level**   
- 프로세서의 core는 프로그램을 다양한 권한으로 실행함(intel : Ring, ARM : EL)
- ARM의 경우 EL0, EL1, EL2, EL3으로 설정하여
- 높을수록 높은 권한을 가짐   
![TrustZone](./images/Trust02.jpg)
- Secure World페이지 테이블의 접근 권한을 설정하는 것이 SCR.NS 레지스터임 이는 EL3에서만 제어 가능함

#### **Design choices w.r.t. threat models**   
- 소프트웨어 공격자
  - 공격자는 유저의 데이터를 노출하고 충돌 시키려 할것이다(캐시 공격)
  - 이를 방어하기 위해 Exception Level 과 NS를 사용하여 접근권한을 제한함
- Trusted IO 를 사용하여 SCR.NS 를 은행 token등을 보호하기 위해 사용
- OS monitoring을 하기위해 TrustZone에서 수행하여 비정상적인 동작을 방어함