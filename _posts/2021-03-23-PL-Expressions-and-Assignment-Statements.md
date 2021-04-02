---
layout: post
title: "[프로그래밍 언어론] 식과 배정문(Expressions & Assignment Statements)"
author: "Soy-A"
comments: true
tags:
- Programming Language
---

# Arithmetic expressions(산술식)

- unary(단항) operator: ++
- binary(이항) operator: + - * /
> 대부분 infix, Perl은 prefix
- tennary(삼항) operator: ? :

---

## Operator evaluation order(연산자 평가 순서)

- 연산자 우선순위: 대부분 parentheses() -> unary -> \*\*(exponent) -> *, / -> +, -
- 연산자 결합 법칙(Associativity): 동일 우선순위, 인접한 두 개의 연산자일 때, 연산자 결합 법칙으로 우선순위 결정
>보통은 left to right: a+b+c -> (a+b)+c<br/>
예외) **: right to left
  - APL은 무조건 R->L, 모든 연산자 우선순위 같다.
  - A+B+C+D -> 수학에서는 어떻게 바뀌어도 상관 없으나 컴퓨터에서는 순서가 바뀌면 overflow / underflow가 발생할 수 있다.  -> not associative하므로
- Parentheses: 괄호로 우선순위, 결합규칙 overide 가능
- 조건식: ?은 자바 조건식에서 tennary로 사용됨

## 평가 과정(순서)
- 변수(variables): just fetch the value
- 상수(constants): sometimes a fetch from memory, sometimes 기계어 명령어의 일부
- 괄호식: 모든 연산자, 피연산자 먼저 평가
- 함수 참조

## 부작용(함수적 부작용)
: 매개 변수 중 한 개나 전역변수 변경시 발생(어떤게 먼저 평가되느냐에 따라 값 바뀜)
> a = 10; b = a + fun(&a);  // fun이 매개변수 변경한다고 가정
1. 함수적 부작용을 허용X<br/>
e.g. No two-way parameters in func, no nonlocal references<br/>
No nonlocal references<br/>
-> 낮은 유연성<br/>
2. 피연산자 평가 순서 정의(fix)<br/>
-> compiler 최적화 제한

### 참조 투명성과 부작용
- 참조 투명성: 동일한 값을 갖는 두 개 식이 프로그램 행동에 영향을 주지 않으면서 프로그램의 임의의 위치에서 서로 다른 식으로 대체가 가능한 것
> e.g. LISP(변수 x 함수 외부: 상수)

> int a, d<br/>
float b = 3.4<br/>
a = 3<br/>
d = b*a<br/>
d = ?<br/>
: a가 확대 변환 통해 float로 변환(3.0), float의 결과를 정수형에 저장하므로 10이 저장됨(narrowing)

## 중복연산자(Overloaded Operators)
- operator overloading: 연산자가 하나 이상의 목적을 위해 사용되는 것
- common: + for int and float
- some are potential trouble( * in C, C++)
> e.g. x = \&y;<br/>
1. 단항 연산자로써 변수의 주소
2. 이항 연산자로써 비트연산 AND

- 에러 검출률 낮아짐
- readability 높아지거나 낮아지거나
- C++은 overload 안되는 연산자 존재(:: - scope resolution op, . - struct member op)
- Java는 연산자 오버로딩 불가



<br/><br/><br/>
**참고 문헌**<br/>
Concepts of Programming Languages, Robert W. Sebesta -10th ed.
