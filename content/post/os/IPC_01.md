---
title: "IPC 01 Overview"
date: 2022-06-06T15:22:15+09:00
author : "Kim Minjae"
description : "ICP os basic"
tags : [
    "system",
    "ICP",
    "OS",
    "C"
]
series : ["OS"]
---
## IPC 통신의 정의와 필요성
프로세서가 independent 하게 동작할때 문제가 되지 않는다. 그러나 프로세서가 서로의 데이터를 주고 받을때 문제가 생긴다. 이를 해결하기 위해서 데이터를 주고 받는 방법이 필요하다.
두가지 모델이 있음
1. shared memory : 두프로세서가 공유하는 메모리 공간을 사용하는 방법    
2. message passing : 운영 체제에서 프로세서 간의 데이터를 주고 받는것게 개입하는 방법

IPC 통신에서 고려해야할 문제는 Producer-Consumer problem이다. 생산자는 생산품에 대한 정보를 소비자에게 알려줘야한다는 문제를 가지고 있다.

### shared memory 해결 방법
공급자와 소비자가 동시에 실행된다고 했을때 서로 공유하는 메모리 공간에 버퍼를 사용한다고 가정하고, 공급자는 버퍼를 채우고, 소비자는 버퍼를 비운다고 한다.
이때 공유하는 메모리 공간은 공급자, 소비자 프로세서면 사용가능하게 한다.
```c
#define BUFFER_SIZE 10

typedef struct {
    ...;
}item

item buffer[BUFFER_SIZE];
int in = 0;
int out = 0;
```
위 코드와 같이 하나의 버퍼를 생산자와 소비자가 같은 포인터 값(사용하는 데이터의 위치)를 사용함

```c
/* producer proccess shared memory*/
item next_produced;

while(true){
    while(((in + 1) % BUFFER_SIZE) == out);

    buffer[in] = next_produced;
    in = (in + 1) % BUFFER_SIZE;
}
/* consummer proccess shared memory*/
item next_consumed;

while(true){
    while(in == out); // do nothing

    next_consumed = buffer[out];
    out = (out + 1) % BUFFER_SIZE;
}
```

### shared memory 방법의 문제점

메모리 영역에 대한 액세스 권한 설정과 관리를 프로그래머가 구현해야함
그래서 프로세서가 늘어나고, 하나의 메모리 영역을 여러개의 어플리 케이션이 공유할 경우 아주 복잡한 문제가 생길 수 있음

### message passing 방식

O/S가 cooperating processed 에게 서로간에 메세지를 주고 받을 수 있는 수단을 제공함
2개의 메소드를 사용해서 사용함
- send(message)
- receive(message)

두개의 커뮤니 케이션 링크를 사용해서 데이터를 주고 받으며 여러가지 옵션이 존재함
 - direct / indirect
 - synchronous / asynchronous

**blocking send** : 송신측에서 수신측이 데이터를 읽기 전까지 blocked 되는 것을 의미한다

**Non-blocking send** : 송신측은 메세지를 보내고 가만히 있는것을 의미

**synchronous** : 동시에 진행 된다는 의미로, 결과가 나오지 않는다면 뒤의 작업을 진행하지 않는다는것을 의미한다

**asynchronous** : 동시에 똑같이 진행되지 않는다는 의미, 작어블의 요청과 응답의 타이밍이 같지 않아도 된다는 것을 의미한다.