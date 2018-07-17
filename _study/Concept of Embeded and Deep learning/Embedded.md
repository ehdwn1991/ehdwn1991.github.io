---
layout: post
title: 임베디드 시스템 기초
comments: true
description: >
  임베디드 시스템 기초, ARM 동작 원리, 메모리 구조, 운영체제

study: [study_coe]
tags: [c]
date: 2018-07-13
author: author2
---



## Embedded System?

> An embedded system is a computer system --- 작은 컴퓨터 라고 생각하자.
>
> Dedicated function --- 시스템에 맞춰 특정 동작을 한다.
>
> Within a lager mechanical or electronical system  
>
> 더 큰 시스템의 일부로 내장(embedded)된다.
>
> 큰 시스템 안에 여러개의 임베디드 시스템이 동시에 존재할 수 있다.

- Characteristic of Embedded system
  - 특정 기능을 수행
  - 하드웨어 + 소프트웨어로 구성
  - 하드웨어 변경 쉽지 않음
  - 제한적인 자원
  - 고 신뢰성, 실시간성의 요구



## SoC

> SoC(System on chip) 은

![soc 참고](https://upload.wikimedia.org/wikipedia/commons/8/85/ARMSoCBlockDiagram.svg)