---
layout: post
title: (Backjoon) 수학 알고리즘
comments: true
description: >
  백준 수학 알고리즘

  [모든 내용은 Git Hub에도있습니다.](https://github.com/ehdwn1991/Codex/tree/master/backjoon/Math_prob)
categories: [backjoon]
tag: [c,backjoon_class]
author: author2
---

## Math Problem
{:.no_toc}
* 
{:toc}

## [알고리즘 분류[수학]](https://www.acmicpc.net/problem/tag/%EC%88%98%ED%95%99)


### [1978번 문제](https://www.acmicpc.net/problem/1978)
```shell
소수찾기
소수는 sqrt(N)까지만 검색하면 된다. 2~sqrt(N)까지 나누어 떨어지는 수가 없다면 소수가 보장되기 때문임.
```
```c
#include <stdio.h>
#include <math.h>
int is_prime();
int main(){
	int N,input,count=0,prime=1; 
	scanf("%d",&N);
	for (int i = 1; i <= N; ++i)
	{
		// input=i;
		scanf("%d",&input);
		if(is_prime(input)==1)
			count++;
	}
	printf("%d\n",count);
}
int is_prime(int num){
	if(num==1)
		return 0;
	for (int j = 2; j <= sqrt(num); ++j)
	{
		if(num%j==0){
			return 0;
		}
	}
	return 1;
}
```


### 에라토네스의 체 알고리즘

```c
/*
에라토스테네스의 체 알고리즘을 기준으로 찾는다.
2부터 소수를 구하고자 하는 구간의 모든 수를 나열한다. 그림에서 회색 사각형으로 두른 수들이 여기에 해당한다.
2는 소수이므로 오른쪽에 2를 쓴다. (빨간색)
자기 자신을 제외한 2의 배수를 모두 지운다.
남아있는 수 가운데 3은 소수이므로 오른쪽에 3을 쓴다. (초록색)
자기 자신을 제외한 3의 배수를 모두 지운다.
남아있는 수 가운데 5는 소수이므로 오른쪽에 5를 쓴다. (파란색)
자기 자신을 제외한 5의 배수를 모두 지운다.
남아있는 수 가운데 7은 소수이므로 오른쪽에 7을 쓴다. (노란색)
자기 자신을 제외한 7의 배수를 모두 지운다.
위의 과정을 반복하면 구하는 구간의 모든 소수가 남는다.
*/
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
int main(){
	int N,count=1;
	scanf("%d",&N);
	char *arr=(char*)malloc(sizeof(char)*N);
	memset(arr,1,sizeof(char)*N);
	puts(arr);
	for (int i = 2;  (i*i)<= N; ++i) //루트 N까지만 체크
	{
		if(arr[i]==1){
			for (int j = i*i; j < N; j+=i)
			{
				arr[j]=0;//1 is prime 0 is not prime
			}
		}

	}

	for (int i = 2; i < N; ++i)
	{
		if(arr[i]==1){
			printf("%d ",i);
		if(count%10==0)
			puts("");
		count++;
		}
	}
		free(arr);
}
```

### Pascal Triangle
`파스칼 삼각형`
```c
#include <stdio.h>
#include <stdlib.h>
int main(){
	int N;
	scanf("%d",&N);
	int **row;
	row=(int**)malloc(sizeof(int*)*N);

	for (int i = 0; i < N; ++i)
	{
		row[i]=(int*)malloc(sizeof(int)*((N*2)-1));
	}
	for (int i = 0; i < N; ++i)
	{
		for (int j = 0; j < i+1; ++j)
		{
			if(j==0||j==i){
				*(*(row+i)+(N-1+(j*2)-i))=1;
			}
			else{
				*(*(row+i)+(N-1-i+(j*2)))=(*(*(row+i-1)+(N-1-i-1+(j*2))))+(*(*(row+(i-1))+(N-1-i+(j*2)+1)));
			}
		}
	}
	for (int i = 0; i < N; ++i)
	{
		for (int q = 0; q < (N*2)-1; ++q)
		{
			if(*(*(row+i)+q)%2==1)
			// if(*(*(row+i)+q)!=0)
				printf("%d",*(*(row+i)+q));
			else{
				printf(" ");
			}
		}
		free(*(row+i));
		puts("");
	}
}
```


[모든 내용은 Git Hub에도있습니다.](https://github.com/ehdwn1991/Codex/tree/master/backjoon/Math_prob)