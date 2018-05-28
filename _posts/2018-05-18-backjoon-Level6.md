---
layout: post
title: (Backjoon) 단계별 문제 풀이 Level 06
comments: true
description: >
  백준 단계별 문제집 레벨6
  
  [모든 내용은 Git Hub에도 있습니다.](https://github.com/ehdwn1991/Codex/tree/master/backjoon/Level_6)
categories: [backjoon]
tag: [c,backjoon_level]
author: author2
---
## Level6
{:.no_toc}
* 
{:toc}

## [1152번[단어의 개수]](https://www.acmicpc.net/problem/2577)

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
int main(){

	int count=0,is_word=0;
	//is_word=0 =>until not using any word
	//is_word=1 =>wherever used any word before using space
	char input;
//공백은 연속으로 나오는 일이 없으니 공백만 잘 체크해 주면 된다.
	while((input=getchar())!=EOF){
		if(input==10){
			if(is_word==1)
				count++;
			break;
		}
		if(input>32){
			is_word=1;
		}
		else{
			if(input==32&&is_word==0){//is space
			}
			else if(input==32&&is_word==1){
				count++;
				is_word=0;
			}
		}
	}
	printf("%d\n",count );
}
```
>문제에서 헷갈리는 부문이 있다.
>1.시작이 공백
>2.끝이 공백
>두가지 경우를 어떻게 처리할것인가가 좀 헷갈렸다.
>[시작이 공백]
>		시작이 공백이고 아직 단어가 한번도 안나온 경우
>		시작이 공백이지만 이미 단어가 한번 나온경우
>[끝이 공백]
>		마지막 문자가 Newline이고 is_word가 1이라면 이전에 글자가 있었던것


## [2257번[숫자의 개수]](https://www.acmicpc.net/problem/2577)
```c
#include <stdio.h>
int main(){
	int a,b,c,multi;
	int count[10]={0,};
	scanf("%d",&a);
	scanf("%d",&b);
	scanf("%d",&c);
	multi=a*b*c;
	while(multi>0){
		count[multi%10]+=1;
		multi/=10;
	}
	for (int i = 0; i < 10; ++i)
	{
		printf("%d\n",count[i]);
	}
}
```


## [8958번[OX퀴즈]](https://www.acmicpc.net/problem/8958)
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main(){
	int now_point=0,total_point=0;
	int count=0;
	char buf[81]={'\0',};
	scanf("%d",&count);
	while(getchar()!=10);
// 입력 버퍼를 비워 주지 않으면 테스트 횟수 입력후 첫번째 케이스 문자가 입력이 안됨
// 왜냐면 처음 반복 횟수 입력후 버퍼의 상태는 N\n 이렇게 들어있음 즉 숫자와 엔터가
// 들어있는 상태임 그래서 그다음에 fgets 를 쓰려고 하면 입력이 끝나 버리는것
//그래서 두가지 방법중 하나를 써줘야됨
//1.scanf("%d ") => 공백을 하나 추가하여 
//2.while(getchar()!=10) \n 이 나올때까지 입력 버퍼를 비워줌
	for(int i=0;i<count;i++){
	fgets(buf,sizeof(buf),stdin);
	for(int j=0;j<strlen(buf);j++){
	if(buf[j]=='O'){
	++now_point;
	total_point+=now_point;
	}
	if(buf[j]=='X'){
	now_point=0;
	}	
	}
	printf("%d\n",total_point);
	total_point=0;
	now_point=0;
	memset(buf,'\0',strlen(buf));
	}
}
```
>알고리즘은 간단하다. 근데 입출력에 문제가 생겼음.
>scanf로 입력 받았을때는 버퍼의 마지막에 '\n' 이 있는 상태이고
>그다음에 바로 getchar를 쓴다면 버퍼 마지막의 '\n'을 가져 오게 된다
>그래서 첫번째 케이스의 첫 글자가 입력이 안되서,
>scanf로 입력 받고 버퍼를 비워줘야함.


## [2920번[음계]](https://www.acmicpc.net/problem/2920)
```c
#include <stdio.h>
int main(){
	int temp[8]={0,};
	int state[8]={0,};
	int now_state;
	// 0=ascending 1=descending 2=mix
	for(int i=0;i<8;i++){
	scanf("%d",&temp[i]);
	}
	now_state=temp[1]-temp[0];
	for(int j=0;j<7;j++){
		if(now_state==1&&now_state==(temp[j+1]-temp[j]))
		//오름차순
			continue;
		else if(now_state<0&&now_state==(temp[j+1]-temp[j]))
		//내림차순
			continue;
		else{
			now_state=2;
			//등차 수열을 이루지 못해서 Mix의 상태임.
		break;
		}
	}	
	if(now_state==1)
		printf("ascending\n");
	else if(now_state<0)
		printf("descending\n");
	else
		printf("mixed\n");
}
```
>시작이 1 혹은 8 둘중하나로 시작 하면 오름차순 이거나 내림차순 일것이다.
>즉 하나의 수열로 봤을때 등차 수열이 되야한다는것.
>등차 수열을 이루지 못하다면 Mix 인것이다.


## [100039번[평균점수]](https://www.acmicpc.net/problem/100039)
```c
#include <stdio.h>
int main(){
	int a;
	int temp[5]={0,};
	int total=0;
	for(int i=0;i<5;i++){
		scanf("%d",&temp[i]);
		if(temp[i]<40)
			temp[i]=40;
		total+=temp[i];
	}
	printf("%d\n",total/5);
}
```


[모든 내용은 Git Hub에도 있습니다.](https://github.com/ehdwn1991/Codex/tree/master/backjoon/Level_6)

