---
layout: post
title: (Backjoon) 단계별 문제 풀이 Level 17
comments: true
description: >
  백준 단계별 문제집 레벨17  
  
  [모든 내용은 Git Hub에도있습니다.](https://github.com/ehdwn1991/Codex/tree/master/backjoon/Level_17)
categories: [backjoon]
tag: [c,backjoon_level]
author: author2
---
## Level17
{:.no_toc}
* . 
{:toc}
## [10871번[윷놀이]](https://www.acmicpc.net/problem/2490)
자세한 설명 [여기](2018-05-18-backjoon-Level4.md) 참고
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main(){

	int input[10000];
	int N=0,X=0,insert_num=0;
	scanf("%d %d\n",&N,&X);
	for(int i=0;i<N;i++){
		scanf(" %d",&insert_num);  //scanf의 심오한 의미 공부!!!
		input[i]=insert_num;
	}

	for (int i = 0; i < N; ++i)
	{
		if(input[i]<X)
		printf("%d ",input[i] );
	}

}
```

## [2490번[윷놀이]](https://www.acmicpc.net/problem/2490)
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(){

	int bae,deung;
	int one,two,three,four;
	char buf[10];
	int status_zero=0,status_one=0;
	for(int i = 0; i < 3; ++i){
		fgets(buf,sizeof(buf),stdin);
		for (int j = 0; j < strlen(buf); ++j)
		{
			if(buf[j]=='0')
				status_zero++;
			else if(buf[j]=='1')
				status_one++;
			else
				continue;
		}

		if(status_zero>0){
			switch(status_zero){
				case 1:
				printf("A\n");
				break;
				case 2:
				printf("B\n");
				break;
				case 3:
				printf("C\n");
				break;
				case 4:
				printf("D\n");
				break;
			}
		}
		else
			printf("E\n");
	status_one=0;
	status_zero=0;
	}
}
```
[모든 내용은 Git Hub에도있습니다.](https://github.com/ehdwn1991/Codex/tree/master/backjoon/Level_17)