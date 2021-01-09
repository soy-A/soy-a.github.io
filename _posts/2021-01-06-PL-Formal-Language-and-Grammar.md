---
layout: post
title: "[프로그래밍 언어론] 형식 언어와 문법"
author: "Soy-A"
comments: true
tags:
- Programming Language
---

# 형식 언어

## 용어 정리

### 알파벳

- **알파벳** Σ(시그마)은 유한하고, 공백이 아닌 심볼들의 집합을 말한다
> e.g. 이진수: Σ = {0, 1}<br/>
모든 소문자(영어): Σ = {a, b, c, ..., z}

---

### 문자열

- 알파벳(Σ)으로 부터 얻어지는 **심볼들의 유한한 연속**을 말한다
> 빈 문자열(길이가 0인 문자열)은 ε(입실론)으로 표현한다<br/>
Σ = {a, b, c} -> 문자열: a, ab, ccba, ...
- 문자열의 길이: \|s\| (s은 문자열)
- xy는 문자열 x와 y의 연쇄이다
> e.g. x = abcd, y efgh -> wy = abcdefgh
- a^n = a...a (n개의 a가 연쇄)

---

### 알파벳의 지수
- ∑k : 길이가 k인 모든 문자열의 집합을 나타냄
- ∑* : 모든 길이의 문자열의 집합들의 합집합
- ∑+ :  ∑*에서 ε을 제외한 것
>  ∑ = {a,b,c}<br/>
∑^2 = {aa, bb, cc, ab, ba, ac, ca, bc, cb}<br/>
∑* = {ε,a,b,c,aa,bb,cc,ab,ba,ac,ca,bc,cb,aaa,...}<br/>
∑+ = {a,b,c,aa,bb,cc,ab,ba,ac,ca,bc,cb,aaa,...}

---

### (형식) 언어
- 어떠한 알파벳 Σ에 대한 언어는 **∑*의 부분집합**이다 (L ⊆ ∑*)
> ∑ = {a,b}<br/>
L1 = {a, ba, bbbb} #유한한 언어<br/>
L2 = {a^p | p는 소수} #무한한 언어<br/>
     = {a, aa, aaa, aaaaa, aaaaaaa, ...}

<br/><br/>

# 문법

### 문법이란?
- 적법한 문자열을 생성하도록 하는 **규칙에 따라 언어를 명세**한 것
> e.g. S -> dingdongA	# S는 dingdongA라는 문자열을 나타낸다<br/>
A -> dengS | deng		# A는 dengS 또는 deng이라는 문자열을 나타낸다<br/>
S -> dingdongA -> dingdongdeng<br/>
S->dingdongA->dingdongdengS->dingdongdengdingdongA-> dingdongdengdingdongdeng<br/>
...
- 위의 문법에 따르면 이 언어는 dingdongdeng을 한 번 이상 포함하게 된다<br/>
L = {(dingdongdeng)^n | n ≧ 1}

---

### (형식) 문법

- 형식 문법은 **G = (VN, VT, P, S)**로 표현한다
 - VN: 비말단(non-terminal) 기호들의 유한한 집합
 - VT: 말단(terminal) 기호들의 유한한 집합
 - P: 생성 규칙의 집합
 - S: 시작 기호

---

### 문법의 표기법

- non-terminal 기호: 대문자 사용
-  terminal 기호: 소문자
-  시작 기호: S

---

### 유도(derivation, ⇒)

- 한 문자열에서 생성 규칙을 한 번 적용해서 다른 문자열로 바꾸는 것
- →: 생성 규칙에서 사용
- ⇒: 유도를 나타낼 때 사용

---

### 문법으로부터 생성된 언어

- 문법 G = (VN, VT, P, S)로부터 생성된 언어는 **L(G)**로 표기되는 집합이다
- L(G)={w|w ∈ VT* and S ⇒* w}

<br/><br/>

# 촘스키 계층 구조(The Chomsky Hierarchy)
- G = (VN, VT, P, S)에서 **P에 제약**을 건 것

---

### 형식 언어의 네 가지 타입

#### Type0

- 무제약 문법(unrestricted grammar)
- 생성규칙에 아무런 제약이 없다
> α→β
- 인식 오토마타: 튜링 머신(Turing machine)

#### Type1

- 문맥 의존 문법(context-sensitive grammar)
- 항상 lhs가 rhs보다 길이가 작거나 같아야 한다
> α→β, **|α| ≦ |β|**, α ∈ V+, β ∈ V*
- 인식 오토마타: 선형 구속형 오토마타(Linear bounded automata)

#### Type2

- 문맥 자유 문법(context-free grammar)
- lhs에는 반드시 하나의 non-terminal 심볼만 올 수 있다
- BNF: context-free grammar
> α→β, **α ∈ VN**, β ∈ V*
- 인식 오토마타: 푸시다운 오토마타(Pushdown automata)

#### Type3

- 정규 문법(regular grammar)
> 오른쪽 정규 문법: α → tβ | t<br/>
왼쪽 정규 문법: α → βt | t<br/>
α , β ∈ VN , t ∈ VT*
- 인식 오토마타: 유한 상태 오토마타(Finite automata)

각각의 오토마타는 주어진 문자열이 어떤 문법인지를 판단한다

<br/><br/><br/>
**참고 문헌**<br/>
Concepts of Programming Languages, Robert W. Sebesta -10th ed.