---
layout: post
title: "[프로그래밍 언어론] 데이터 타입"
author: "Soy-A"
comments: true
tags:
- Programming Language
---

- 데이터 타입(data type): 데이터 값들의 모임과 그들 값들에 대한 미리 정의된 연산들의 집합을 정의
- 서술자(descriptor): 변수의 속성들의 모임
  - 구현(implementation)에서, 서술자는 변수의 속성들을 저장하는 메모리의 영역을 의미
  - 모든 경우, 서술자는 타입 검사를 위해 사용되고 할당(allocation)과 회수(deallocation) 연산을 위한 코드를 생성하는데 사용됨


# 기본 데이터 타입(primitive data types)

- 다른 타입들의 관점에서 정의되지 않은 데이터 타입

---

## 수치 타입(numeric types)

- 초기의 많은 프로그래밍 언어들은 수치(numeric) 기본 타입들만 제공
- 여전히 중심적인 역할

#### 정수(integer)

- 가장 공통된 기본 수치 데이터 타입
- 대부분의 정수 타입은 하드웨어에 의해 직접 지원됨
- Java: byte, short, int, long
- C++, C#: unsigned integer
- 음의 정수 표기법
  - 부호-크기 표기법(sign-magnitude notation)
  - 1의 보수(one's complement)
  - 2의 보수(two's complement)

#### 부동-소수점 수(floating point)

- 실수를 모델링하지만, 그 표현은 단지 대부분의 실수 값에 대한 근사 값임
- 포맷: IEEE Floating Point Standard 754
- 대부분의 언어는 두 가지 부동-소수점 수의 타입을 포함: float, double
- 대체로 하드웨어와 같지만 항상은 아님
- 부동-소수점 수 타입으로 표현될 수 있는 값들의 집합은 정밀도(precision)와 범위(range)의 관점에서 정의됨



<br/><br/><br/>
**참고 문헌**<br/>
Concepts of Programming Languages, Robert W. Sebesta -10th ed.