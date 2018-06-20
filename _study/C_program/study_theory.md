---
layout: post
title: C언어 스터디
comments: true
description: >
  수업 내용 중요부분 집중 정리!!!
study: [study_lang_c]
tags: [c]
date: 2018-06-11
author: author2
---
* 
{:toc}
# C언어
{:no_toc}

프로그램이란? 컴퓨터에서 실행될때 특정 작업을 수행 하는 일련의 명령어들의 모음이다.

## 소프트웨어 공학

  - 요구사항 분석
    자료형 정의 등등
  - Flow chart 설계 및 구현(pseudo code)
  - 코드 구현
  - 실행
  - 테스트
  - 유지보수
## CPU 구조

  Control unit<->ALU<->Processor resister(R1,R2,R3...)
  위의 3가지 장치들이 Internal bus로 연결되어 통신한다.

  - ALU(Arithmetic logic unit )

    산술 논리 장치 : 실질적으로 산술, 논리 계산을 수행함.

  - Resister

    CPU의 자체적인 메모리저장 기능.

    Memory buffer register(MBR)

    ​	I/O로 보내지거나 메모리에 저장될 Word 혹은 I/O나 메모리로 부터 Word를 받는 것. 

    Memory address register(MAR)

    Instruction register(IR)

    Instruction buffer register(IBR)

    Program counter(PC)

    Accumulator (AC) and mutiplier quotient (MQ)

  - Control unit

    CPU의 명령어를 제어한다.


## 폰노이만 구조(최초의 컴퓨터 구조를 만듬)

  폰노이만의 구조는 CPU, 메모리, 프로그램 구조를 갖는 프로그램 내장 방식 컴퓨터를 뜻한다.


![cpu구조](https://upload.wikimedia.org/wikipedia/ko/a/a1/Von_Neumann_architecture_kor.png){: .center-image}
<center>폰노이만 구조(출처: 위키 백과사전)</center>



## C 메모리 구조

![c메모리 구조](https://1.bp.blogspot.com/-DoCFzIcQGDs/VlnGRLw69mI/AAAAAAAAAz0/xxrtrqK39FU/s1600/process%2Blooks%2Bin%2Bmemory.jpg){: width="50%" height="50%"}<center>(출처 : https://bitsofcomputer.blogspot.com/)</center>

  c언어에서의 메모리 구조를 알고 있다는것은 상당히 중요하다.

  주로 동적 할당 할때나 임베디드 시스템을 다룰때 메모리 구조와 영역을 알고 있으면 편하다.

  [geeks를 참고 하면서 공부해보자](https://www.geeksforgeeks.org/memory-layout-of-c-program/)

  

## 컴파일 과정

- gcc compiler

  source.c -------> source.i -------> source.s -------> source.o -------> source

  ​         (precompile)       (compiler)         (assembler)           (linker)

![gcccompile](https://www3.ntu.edu.sg/home/ehchua/programming/cpp/images/GCC_CompilationProcess.png)
<center>gcc compile 과정 (출처: 제타위키)</center>

```shell
$ gcc test.c
$ ls
 a.out 실행 파일 생성
$ gcc -c test.c
 test.o 오브젝트 파일 생성
$ gcc -o test.out test.o 
 test.out 실행 파일이 생성됨
$ gcc -v --save-temps -o test.out test.c 컴파일 전체 과정을 보여주고 파일을 저장해줌
	test.c test.i test.s test.o test.out
```

## 상수, 변수

- 변수(Variable) : 정수, 실수, 문자, 문자열 등의 형태를 갖춘 가변 데이터.

- 상수(Constant) : 값이 바뀌지 않는 데이터를 상수라 한다.

  1. 변수 상수화

     변수 앞에 const를 붙여주면 상수가 된다.

     const int a; => 상수로 정해진 변수는 값을 바꾸는것이 불가

  2. 매크로를 통한 상수화

     `# define` 을 통해서 상수를 만들수 있다. 매크로는 전처리기에 의해 변환 되고

     전역변수 처럼 사용 가능 하다. 위치는 헤더 파일 제일 밑에 사용해주면된다.

     ```c
     #include <stdio.h>
     #define pi 3.14
     #define poweroftwo 2
     ```

     

  ex) 정수 상수 => -2,-1,0,1,2,3....

  ​      실수 상수 => -1.2, -0.2231, 3.14...

  ​      문자 상수 => '1', '2' ,'ㄱ','A','a'...

  ​      문자열 상수 => "abc", "ABC"...

  1. 정수형 상수의 컴파일후의 비트 형태

     정수형 상수는 컴파일되면 4바이트 크기의 2진수 형태로 변환 된다.

     예를 들어 정수 13이 컴파일 되면, 나머지 비트는 0으로 채워 지게 됩니다.

     ```c
     0000 0000  0000 0000  0000 0000  0000 1101
     <--MSB                              LSB-->
     ```

     여기서 중요한 개념이 나옵니다. MSB와 LSB가 무었인가

     MSB는 `Most significant bit` 라 하며 가장 왼쪽의 비트는 전체 값에서 가장 큰 비중을 차지한다.

     LSB는 `Least significant bit` 라 하며 가장 오른쪽의 비트는 전체 값에서 가장 작은 비중을 차지한다.

     예를 들어,

     ```c
     1000 0000(128)  >  0111 1111(127)
     극단 적인 예로 128과 127의 차이를 보면된다.
     뇌피셜로는 비트가 1인 비트가 많을수록 숫자가 크다.
     물론 맞는 말이지만 모든경우에 해당되지는 안는다.
     위의 예처럼 오른쪽 7비트가 전부 1인 값보다 가장 왼쪽 1비트가 1인 값이 크다.
     ```

     그렇다면, 비트가 큰값으로 움직일때는 MSB의 움직임을 보면될것이다. 만약 작은 단위로   

     비트가 움직여야 한다면, LSB를 보면 되는데 이때 한가지 예를 살펴봐야 한다.

     ```c
     (0x8E)1000 1101(141)   -->   (0x8D)1000 1110(142)
     1가장 왼쪽 LSB의 1비트 움직임을 보일때 Niddle단위로 비트가 이동한다고 한다.
     ```

  2. 실수형 상수의 컴파일후의 비트 형태

     single, double, quad 세가지 형태가 있고, 그중에서 double형태를 살펴본다.

     ```c
       0          00000000000      00000...       
     부호비트(1)   지수 저장 비트(11)	  소수 저장 비트(52) => 8byte(64bit) 
      //소소부
        1    1    1  ...
      2^-1 2^-2 2^-3 ...
      위의 예시처럼 소수부는 2의 -n제곱의 형태를 띈다.
      때문에 소수르 사용한 계산은 정확하지 안을수 있다.
      2^-1 => 1/2 이고 0.5이다.
      2^-2 => 1/4 이고 0.25이다
      2^-3 => 1/8 이고 0.125이다.
      소수부분이 5의 나머지 연산으로 처리 되는점을 보면, 0.3 같은 표현은 다루기 힘들다.
     ```

     

     

## 강제 형변환 vs 자동 형변환


  - 자동 형변환

    자동 형변환은 더 작은 자료형에서 더큰 자료형으로 assign할때 발생.

    ```c
    int a=8,b=2;
    double b=a/b;
    printf("%f\n",b);
    //실행결과
    4.000000
    ```

    우리가 원하는 값은 4였을 터이지만 실제 출력값은 4.000000이 나온다.

    double은 8바이트를 할당하고 지수부분에 11비트 소수부분이 52비트를 저장한다.

    때문에 지수부분 4와 소수부분 52비트 즉 6바이트 0.000000 이기 때문에  

    소수점 밑으로 6자리를 표기한다.

  - 강제 형변환

    위와 같은 경우에서 원하는 값인 2로 표기할수도 있다.

    ```c
    printf("%d",(int)b);
    //실행결과
    4
    ```

    물론 강제 형변환은 포인터 에서도 많이 쓰인다.

    [함수 포인터](), [byte access](/study/lecture0615/#1byte-access) 를 참고.

## 전달 인자(Argument)와 매개변수(Parapeter)

```c
int   *a  =  &temp;
	매개변수   전달인자
int add(int *a){}
         매개변수
add(&temp);
    전달인자
```



## LIttle and Big Endian

```c
int a=1; => 0x 00 00 00 01
   Little    Big
|___01___|___00___| 0x7fff2ab9
|___00___|___00___|
|___00___|___00___|
|___00___|___01___|
|________|________|
```

시스템마다 little endian, big endian 두가지 방법중 하나를 채택한다.

하지만 다양한 종류의 컴퓨터들끼리 통신을 해야 하는데, 이때 데이터를 읽어서 저장하는 방법이  

다르다면 문제가 생긴다 때문에, 한가지로 통일해 줘야 한다.

이떄 사용 되는 방법이 [Byte Access](/study/lecture0615/#1byte-access)이다

## Digital logic circuit(DLD)





## Bitwise

* 특정 비트 on/off

  예를들어 Led의 한부분을 껏다 켯다 하는 동작이 발생할수도 있다.

  LED와 연결되어 있는 특정 주소의 값에 한 비트를 on/off해야 동작 할때

  다음과 같은 비트 연산으로 수행 가능하다.

  ```c
  res => 0x 1111 0111
  res&=~(0x01 << 7);
    0111 1111 (~res)
  & 1111 0111 (res)
  _____________
    0111 0111 => 가장 오른쪽 1비트만 off가 되었다
  이처럼 특정 비트를 on/off할때에 ~(not)과 &(and)연산이 필요하다.
  ```

  



## Basic of Loop

프로그래밍중에 실수와 의도에 의해서 무한 루프가 발생하거나 써야 하는 일이 있다.

1. 의도치 않은 무한 루프

   대부분 세미 콜론이나, 조건식을 잘못 써서 발생한다.

   ```c
   //case1
   int val=0;
   while(val<5); => while문의 내용이 시작하기 전에 세미콜론을 사용하였다.
   {
       printf("a\n");
   }
   
   결과는 물론 무한 루프이다.
   while 문의 조건식을 잘못 적용 하였고 루프에 빠지게 될텐데,
   while 문의 내용이 시작하기 전에 세미 콜론으로 마무리 했다.
   때문에 printf 는 while 문의 무한 루프 때문에 출력이 되질 않는다.
   //case2
   int val=0;
   for(val=0;val<5;val++); => for문의 내용이 시작도 전에 세미콜론이 찍혔다.
   {
   printf("aa\n");
   }
   이번엔 어떨까? aa가 5번 찍히는가? 아니다.
   for문의 내용이 시작도전에 세미콜론이 있기 때문에, for문만 5번 돌아가고나서
   printf 는 한번만 사용된다. 즉 aa는 한번만 출력되는것!!
   그럼 중괄호('{}')의 역할은 뭘까?
   보통 중괄호는 코드의 영역을 나타낸다.
   ```

2. 의도한 루프

   Firmware 등의 기본 동작에 필요한 경우가 있다. 혹은 지연 시간을 위해 고의적으로 넣는 경우도  

   있는데, 지금은 펌웨어에서 필요로 하는 Polling 방식에 대해 기술해 보려 한다.

   * Polling

     폴링방식은 하나의 프로그램에서 상태를 주기적으로 체크하여, 조건에 해당될때 송수신하는 목적이다.

     예를 들어 보자, 세탁기 같은 내장프로그램을 봤을때, 시작과 종료 후에 다시 시작을 눌러도  

     기계는 작동한다. 이는 폴링 방식에 의해서 주기적으로 루프를 돌고 있기 때문이다.

     ```c
     while(1){
         조건1
         조건2
         조건3
         ...
     }
     프로그램은 계속해서 주기적으로 조건이 만족한 명령을 수행후 다시 while 문 의 처음으로
     돌아와서 처리한다.
     ```

     

   * Interrupt

     인터럽트 방식은 특정 이벤트가 발생했을때 동작을 멈추고 해당 이벤트를 처리하는것

     주로 OS를 대표적인 예로 들수 있다. 만약 종료라는 이벤트가 발생한다면, cpu는 그즉시

     모든 연산을 멈추고 종료를 처리한다.

     물론 인터럽트 방식은 예기치 못한 상황에 대비할때 좋은 방법이다.

## Array

배열은 자료형의 집합이라고 생각할수 있다.

```c
int arr[5];
여기서 int 는 배열의 자료형이고
arr은 배열명이다.
```

이제는 배열을 활용하는법을 알아야 한다.

배열에 접근해서 직접 자료를 처리해서 프로그래밍을 해야한다.

때문에 배열에 접근 하는 방법을 알필요가 있다.

1. 직접 접근(Direct access)

   배열에 직접적으로 접근하는 방법이다.

   ```c
   arr[0]=5;
   printf("%d\n",arr[1]);
   ```

   

2. 간접 접근(Indirect access)

   *(Asteric)에 관한 표현이 나오는데 이는 포인터의 개념이다.

   해당 주소의 값을 가져 온다고 생각 하면 된다.

   ```c
   *arr=5;
   printf("%d\n",*(arr+1))
   ```

이제 배열을 사용하면서 주의해야 할사항들이 있다.

```c
int arr[5];
     arr       !=    arr[0]
배열의 시작 주소       배열의 0번째 값
    *arr      ==   &arr[0]
배열의 시작 주소       배열의 0번째 주소
배열의 시작 주소는 배열의 0번째 주소화 일치한다
```

arr이라는 배열명은 수정 불가능한 포인터 상수이다.

만약  inr arr[5]; 선언후, arr의 주소가 0x2000번지 일때 0x3000번지로 수정하는것 불가!

배열은 한번 스택에 할당 되면 고정된다.

배열의 각 요소 들간의 차이는 배열의 자료형의 크기에 달려 있다.

```c
arr[0]   ->   arr[1]   ->    arr[2]
0x0200  4byte 0x0204  4byte  0x0208
```



## Shallow copy(얕은 복사) vs Deep copy(깊은 복사)

