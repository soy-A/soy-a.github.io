---
layout: post
title: "[프로그래밍 언어론] 구문과 의미론 - 의미론"
author: "Soy-A"
comments: true
tags:
- Programming Language
---

- **구문**(syntax): 표현식, 문장, 프로그램 단위에 대한 **형식**
- **의미론**(semantics): 표현식, 문장, 프로그램 단위에 대한 **의미**

구문과 의미론은 언어를 정의하는 데에 있어 가장 중요한 역할을 한다
<br/><br/>

---

# (동적)의미론
- 언어의 **의미**에 대한 학문
- 상대적으로 단순한 작업인 구문 기술과는 달리, 의미론에 대해서는 보편적으로 채택된 표기법이나 접근 방법 X
- 따라서 세 가지 주요 의미론을 살펴본다
 - **연산 의미론**
 - **표기 의미론**
 - **공리 의미론**

---

## 연산 의미론(operational semantics)

- 문장이나 프로그램의 의미를 **기계상에서 수행되는 효과를 명세**함으로써 기술
- 기계상에서 그 효과는 상태(메모리, 레지스터 등)의 변화 시퀀스로 생각됨
> 한마디로, **언어의 수행 상태 변화**를 기술하는 것

- high-level 언어에 대해 연산 의미론을 사용하기 위해서는 가상 머신(해석기)이 필요하다
> 가상 머신은 중간 언어에 대해서 구성됨

---

## 표기 의미론(denotational semantics)

- 가장 엄격하며, 널리 알려진 의미 기술 방법이다
- **재귀 함수 이론**(recursive function theory)을 기반으로 함
- 언어 구조의 의미는 오로지 프로그램 변수의 값으로만 정의된다

#### 표기 의미론 명세를 구성하는 과정
- 각 언어 요소에 대해 수학적 객체를 정의
- 그 언어 요소의 사례를 해당 수학적 객체의 사례로 매핑하는 함수를 정의

> e.g. **이진수의 문자열 표현 문법 규칙**<br/>
\<bin_num\> -> '0'<br/>
                      \| '1'<br/>
                      \| \<bin_num\> '0'<br/>
                      \| \<bin_num\> '1'<br/>
**파스 트리**<br/>
<img width="338" alt="스크린샷 2021-01-10 오후 9 18 29" src="https://user-images.githubusercontent.com/63772786/104122623-75635080-5389-11eb-827e-7a74352fb102.png"><br/>
**위 이진수의 의미를 표기 의미론을 이용해 기술하면 다음과 같다**<br/>
Mbin( '0' ) = 0<br/>
Mbin( '1' ) = 1<br/>
Mbin(\<bin_num\> '0') = 2 * Mbin(\<bin_num\>)<br/>
Mbin(\<bin_num\> '1') = 2 * Mbin(\<bin_num\>) + 1<br/>
표기된 객체(이 경우 십진수)는 아래와 같이 파스트리의 노드에 부착될 수 있다<br/>
<img width="383" alt="스크린샷 2021-01-10 오후 9 31 31" src="https://user-images.githubusercontent.com/63772786/104122909-38985900-538b-11eb-85f3-e32a1f6c16f0.png">

### 연산 의미론과 표기 의미론의 차이

#### 연산 의미론
- 의미를 기술하기 위해 **기계의 상태**를 사용(e.g. 메모리 상태의 변화)
- 상태 변화가 프로그래밍 언어로 **코딩된 알고리즘**에 의해 정의됨

#### 표기 의미론
- 의미를 기술하기 위해 **프로그램의 상태**를 사용
- 상태 변화가 엄격한 **수학 함수**에 의해 정의됨

---

## 공리 의미론(axiomatic semantics)

- 수학 논리에 기반
- 의미론 명세에 있어 가장 추상적인 접근 방법
- 용도 : 프로그램의 정확성 증명(프로그램이 규격대로 작동하는지를 판단)
- 공리적 의미론에서 사용되는 논리식을 **단언(assertions)**이라고 한다

#### 전조건(precondition)
- 프로그램 문장 **바로 앞**에 위치한 단언
- 프로그램의 그 지점에서 프로그램의 변수들에 대한 **제약 사항**을 기술

#### 후조건(postcondition)
- 프로그램 문장 **바로 뒤**에 위치한 단언
- 그 문장이 **실행된 후** 프로그램 변수들에 대한 **새로운 제약 사항**을 기술

#### 최약 전조건(weakest precondition)
- 후조건의 **유효성을 보장**하는 **최소로 제약된 전조건**
- {P} statement {Q} -> P: 전조건, Q: 후조건
> e.g. **sum = 2 * x + 1 {sum > 1}**<br/>
가능한 한 가지의 전조건: {x > 10}<br/>
최약 전조건: **{x > 0}**<br/><br/>
> **y = 3 * x + 1; x = y + 3; {x < 10}의 최약 전조건**<br/>
**x = y + 3 {x < 10}**에서 후조건을 만족시키기 위한 최약 전조건은 **{y < 7}**이다<br/>
이 최약 전조건은 다음 문장의 후조건이 된다<br/>
-> **y = 3 * x + 1 {y < 7}**에서 후조건을 만족시키기 위한 최약 전조건은 **{x < 2}**이다<br/>
-> {x < 2}

#### 추론 규칙(inference rule)
- 형식: $$ \frac {S1, S2, ..., Sn} {S} $$
- 의미: S1, S2, ..., Sn이 참이면, S가 참이라는 사실이 추론될 수 있다
- 상단 부분: **조건부**(antecedent)
- 하단 부분: **결론부**(consequent)
- **공리**(axiom): 참이라고 가정되는 논리 문장으로, 조건부가 없는 추론 규칙이다

### 배정문
- 배정문: x = E
- 공리: {Q(x->E)} x = E {Q}
- 추론 규칙: $$ \frac {\{P\} S \{Q\}, P' ⇒ P, Q ⇒ Q'} {\{P'\} S \{Q'\}} $$
> ⇒ : "함의한다(imply)"를 의미
- 후조건은 항상 약화될 수 있고, 전조건은 항상 강화될 수 있다는 것을 말함

### 시퀀스 구조
- 시퀀스 S1, S2의 전조건, 후조건:<br/>
{P1} S1 {P2}<br/>
{P2} S2 {P3}
- 추론 규칙: $$ \frac {\{P1\} S1 \{P2\}, \{P2\} S2 \{P3\}} {\{P1\} S1 ; S2  \{P3\}} $$

### 논리 사전-검사 루프(logical pretest loops)
- {P} while B do S end {Q}
- 추론 규칙:  $$ \frac {\{I\ and\ B\} S \{I\}} {\{I\} while\ B\ do\ S \{I\ and\ (not\ B)\}} $$
> I는 **루프 불변자**(loop invariant)

#### 루프 불변자의 조건
- **P ⇒ I** (최약 전조건은 루프 불변자가 참임을 보장)
- **{I and B} S {I}** (I는 루프 실행의 영향을 받지 않아야 함)
- **{I and (not B)} ⇒ Q** (I가 참이고 B가 거짓이면, Q는 함의된다)
- **루프 종료**

> e.g. **while** y \<\> x **do** y = y + 1 **end** {y = x}이 참임을 증명<br/>
\# 첫 번째 '='는 할당의 의미, 두 번째 '='는 같다의 의미임을 주의, \<\>는 같지 않음을 의미<br/>
**1. 루프 불변자 I를 찾는다**<br/>
 iter 0: 최약 전조건: {y = x} (전조건 같아야만 끝나므로)<br/>
 iter 1: wp(y = y + 1, {y = x}) = {y = x - 1}<br/>
 \# 서술자 변환자(predicate transformer): wp(문장, 후조건) = 전조건<br/>
 iter 2: wp(y = y + 1, {y = x - 1}) = {y = x - 2}<br/>
 ...<br/>
 따라서 y는 항상 <= x<br/>
 **y <= x**: 루프 불변자<br/>
**2. 루프 불변자의 조건을 확인한다**<br/>
 -  **P ⇒ I**: 참<br/>
  I: {y <= x}<br/>
 - **{I and B} S {I}**: 참<br/>
  {y <= x and y \<\> x} y = y + 1 {y <= x}로 나타낼 수 있다<br/>
  위의 y = y + 1 {y <= x}는 y + 1 <= x, **y <= x -1**의 조건이 되며,<br/>
  전조건은 **y < x**로 나타낼 수 있다<br/>
  이 둘은 동등하므로 참이다<br/>
 - **{I and (not B)} ⇒ Q**: 참<br/>
  {y <= x and (not y <> x)} ⇒ {y = x}에서 '⇒' 앞의 조건은 {y = x}로 나타낼 수 있으므로 참이다<br/>
 - **루프 종료**: 참<br/>
  정수를 대입함으로써 항상 종료됨을 알 수 있다(어떤 값을 대입하더라도 성립한다)
  
### 공리 의미론의 평가
- 프로그래밍 언어의 어떤 문장에 대해 공리나 추론 규칙을 정의하는 것은 어려운 일
- 프로그램 정확성 증명을 위한 강력한 도구이며, 프로그램을 추론하기 위한 매우 훌륭한 프레임워크임
- but 언어 사용자나 컴파일러 개발자를 위해 프로그래밍 언어의 의미를 기술하는 데 있어서 그 유용성은 상당히 제한됨

<br/><br/><br/>
**참고 문헌**<br/>
Concepts of Programming Languages, Robert W. Sebesta -10th ed.