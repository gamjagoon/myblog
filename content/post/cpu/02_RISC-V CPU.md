---
title: "RISC-V CPU"
date: 2022-07-12T13:55:06+09:00
author : "Kim Minjae"
description : ""
tags : [
    "RISC-V",
    "CPU"
]
series : ["RISC-V CPU"]
---

## RISC-V CPU 설계

CPU는 한번의 사이클에 한번의 명령을 처리하는 single-cycle CPU와 명령어를 여러 단계로 나눠서 처리하는 pipelined CPU가 존재 한다.

일반적으로 보기에는 single-cycle CPU가 빠를거 같지만 하드웨어 관점에 생각한다면 한번의 클럭에 많은 게이트의 지연이 있다고 생각하면 짧은 지연을 가지는 여러개의 단계로 나눠 수행하는것이 면적도 줄어들고 주파수를 높일 수 있어 효과 적이다.

간단하게 Fetch, Decode, Execution 3가지 단계를 파이프 라인으로 수행 한다고 가정한다.

여기서 CPU의 처리량은 단위시간당 처리할 수 있는 명령어의 개수를 의미한다.

### 1.Instruction Fetch 로직 설계

![MPU](/img/IF.png)   
위 그림은 Instruction Fetch 로직이다. Instruction Memory를 읽어 들이는 주소 값을 PC값으로 사용하고며 PC값은 2x1Mux의 Control Signal에 따라 달라진다.


### 2.Decoding 로직 설계

Decoding은 메모리에서 읽어온 명령어를 사용해 control signal을 생성한다. 데이터 연산을 위한 피연산자를 준비한다. pc에 따른 명령어를 읽어오며, 분기 명령어를 수행할 경우 pc값을 변경하는 로직이 추가 된다. 디코딩 로직에서는 opcode를 파싱해서 어떤 타입의 명령어 인지 판단하고, 그 다음 funct3, funct7을 파싱해서 입력한 명령어에 대한 제어 신호를 보낸다.

### 3.Execution 로직 설계

크게 3가지(데이터처리, 분기, 메모리 접근) 동작에 따라 명령어에 따른 data-path가 달리진다.  