---
layout: post
title: 0615 C programing
comments: true
description: >
  
study: [study_lang_c]
tags: [c]
date: 2018-06-12
author: author2
---



## 1Byte access

`강제 캐스팅에 의한 1byte 단위 접근법`

```c
다음과 같이 출력되도록 코드를 짜시오.
temp : 0x12345678
temp : 0x78563412
```

```c
// 강제 캐스팅에 의한 1byte 접근법
#include <stdio.h>

int main(){
	char *s;
	char swap_char;
	int temp=0x12345678;
	s=(char*)&temp; //4byte의 값을 1byte씩 접근
// a=(char)&temp; 변수 자료형의 형변환
	printf("temp : 0x%x\n",temp );
	swap_char=*s;
	*s=*(s+3);
	*(s+3)=swap_char;

	swap_char=*(s+1);
	*(s+1)=*(s+2);
	*(s+2)=swap_char;

	printf("temp : 0x%x\n",temp );
}
```



## Pointer swapping within address

```c
int a=5,b=8;
int *p=&a,*q=&b;

```

