---
title: "01 system security : Intel SGX"
date: 2021-05-25T00:11:34+09:00
author : "Kim Minjae"
description : "x86 Intel SGX description"
tags : [
    "system",
    "security",
    "hardware",
    "Intell",
]
series : ["system security"]
---

---

#### **클라우드 환경**
>
**클라우드 환경의 필요성**   
- 클라우드 환경은 유저를 위해 웹서비스, 파일 저장을 위한 환경을 제공함   
- 클라우드 환경 제공자는 비용 절감을 위해 클라우드를 사용하여 서비스를 제공함   
  - GCP, Azure, AWS 등

**제공자의 신뢰성 문제**   
- 제공받는 데이터 : 유저는 클라우드 제공자의 데이터를 사용함
- 유저의 코드와 데이터 : 클라우드 제공자는 유저의 코드를 유저의 데이터와 같이 실행해야함   
=> 정부 및 군조직, 회사의 보안 데이터

**기존의 환경**   
- 유저 가상머신의 Hypervisor
- 제공자가 제어한는 OS의 컨테이너
- 단순한 계약에 의한 제공자의 데이터 유출과 충돌의 방지
---
#### **Intel SGX 개요**   
>
**ARM 의 TrustZone과 비교**   
- TrustZone : 유저 디바이스에서 서비스의 계산을 수행함   
- Intel_SGX : 공유 클라우드 공간에서 유저의 계산을 수행
- Enclave
  - SGX 가 제공하는 실행환경
  - 개별적인 메모리를 가지고 있음
  - user application과 같은 Privilege level을 가짐


    ![Enclave](https://gamjagoon.github.io/asdf/img/SGX_01.jpg)
    >       <SGX 내부>

**SGX 수행과정**   
1. Client가 App을 클라우드 환경으로 보낸다.
2. App은 Untrusted system에 ㅣoad된다.
3. Enclave에 load 된다
4. code, data의 hash값을 계산하여 Integrity를 생성한다.
5. 클라이언트에게 hash값을 보낸다
6. Client는 기존의 code, data 를 공개키와 비교하여 검증 받는다.   

---

#### **SGX의 한계점**   

- 성능문제
  - 메모리 접근이 느려짐
  - 적은 메모리 공간 사용
- Isolation이 완벽하지 않음
  - Cache timing attack, fault injection에 취약
  - Microcode malicious patchin 공격
  - Untrusted I/O
  - CPU 상에서 일어나는 버그

**메모리가 부족한 이유**   

- SGX는 공격자가 하드웨어 상에서 메모리를 재배치할 가능성이 있어 신뢰하지 않음
- Enclav가 쓰고 읽었다는 것을 확실히 하기위해서 Merkle tree 를 사용함
  - Load : hash 이후 동작
  - Store : hash update가 필요함

    ![Merkle tree](https://gamjagoon.github.io/asdf/img/SGX_02.jpg)
    >       <Merkle tree>

