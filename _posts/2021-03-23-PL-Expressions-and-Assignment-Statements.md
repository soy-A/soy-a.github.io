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



<br/><br/><br/>
**참고 문헌**<br/>
Concepts of Programming Languages, Robert W. Sebesta -10th ed.
