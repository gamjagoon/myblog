---
title: "RISC-V ISA_1"
date: 2022-07-01T17:49:06+09:00
author : "Kim Minjae"
description : ""
tags : [
    "RISC-V",
    "CPU"
]
series : ["RISC-V CPU"]
---

## RISC-V 개요 및 명령어 체계
RISC-V는 버클리대학에서 처음으로 소개한 open standard ISA(Instruction Set Architecture)를 의미한다. 
명령어 집합 구조의 종류는 I,M,B,A,C ... 등 다양하게 존재하며 여기서 제일 기본이 되는 명령어 집합이 I이다. 
명령어, 머신코드는 기계어와 동일한 의다. 이렇게 짜여진 기계어를 CPU가 읽고 명령어를 수행한다. 이렇게 기계어, 머신코드, 명령어를 읽고 동작을 수행하는 CPU의 내부 하드웨어 구조를 마이크로아키텍쳐 라고 한다. 

RV32I에서는 32개의 일반목적 레지스터와 Program Counter가 있다.
RV32I명령어는 R-type, I-type, S-type, U-type 4가지의 기본 형태와 B-type, I-type 등 2가지 파생된 형태로 만들어진다. 각 명령어 형태의 구성은 명령어의 동작을 명시하는 opcode, funct7, funct3 field가 있다. 또한, 어떤 레지스터를 사용하는지와 결과값을 저장하는 field를 rs1, rs2, rd가 있다.

CPU는 크게 3가지의 명령을 수행한다.
* 데이터 처리 명령어
* 메모리접근 명령어
* 분기 명령어