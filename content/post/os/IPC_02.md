---
title: "IPC 02 Shared memory"
date: 2022-06-06T16:30:12+09:00
description : "Shared memory"
tags : [
    "system",
    "ICP",
    "OS",
    "C",
    "shared memory"
]
series : ["OS"]
author : "Kim Minjae"
---
### 01. Shared memory Init

shared memory를 이용한 프로세서 메모리 생성 코드는 아래와 같다
shm_id 값에 KEY_NUM을 사용해 shared memory를 생성하고 받은 shared memory id를 저장한다.
그후 shm_addr에 shm_id를 이용해서 주소값을 받는다.
```c
	shm_id = shmget((key_t)KEY_NUM, (size_t)MEM_SIZE,IPC_CREAT | 0666);
	if(shm_id == -1){
		perror("shmget error :");
		return 0;
	}

	shm_addr = shmat(shm_id, (void*)0,0); 
	if(shm_addr == (void*)-1){
		perror("shmat error :");
		return 0;
	}
```
### 02. Shared memory를 이용한 I/O

(void *)형의 주소값을 받고 이를 사용해서 데이터를 저장한다.   
구조체를 정의하고 void* 형에서 선선한 struct_t *으로 전환하여 데이터 Read/Write를 수행한다.

```c
typedef struct block {
	int player; // 
	int opened; // 
}block_t;

typedef struct blocks{
	block_t block[BLK_SIZE];
	int unuse; // 
	int player_a; // 
	int player_b; // 
}blocks_t;

shm_block = (blocks_t *)shm_addr;
```
