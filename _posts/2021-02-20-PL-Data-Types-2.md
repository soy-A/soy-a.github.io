---
layout: post
title: "[프로그래밍 언어론] 데이터 타입(2)"
author: "Soy-A"
comments: true
tags:
- Programming Language
---

# 레코드(record) 타입

- 개개의 원소들이 이름으로 식별되고, 그 구조의 시작부분으로부터의 오프셋을 통하여 접근되는 데이터 원소들의 집단체
- C, C++, C#에서, 레코드는 **struct** 데이터 타입

---

## 레코드와 배열의 차이

- 레코드의 원소, 즉 필드들(fields)이 색인으로 참조되지 않는다
- 필드들은 식별자로 명칭되며, 필드에 대한 참조는 식별자를 사용
- 어떤 언어에서의 레코드는 공용체(union)를 포함하는 것이 허용됨
- 배열의 원소에 접근하는 것이 레코드 필드에 접근하는 것보다 훨씬 느림(필드 이름은 정적)

## 레코드 필드의 참조

- **완전 자격 참조**(fully qualifed reference)는 가장 큰 포괄적인 레코드부터 특정 필드에 이르기까지 모든 중간 레코드 이름들이 그 참조에 포함된다
> 대부분 도트 표기법(dot notation) 이용
- **생략 참조**(elliptical reference)는 참조가 **모호하지 않은 경우**에 한해 레코드 이름을 생략하는 것을 허용
> in COBOL
>- **full qualified reference**: Middle OF EMPLOYEE-NAME OF EMPLOYEE-RECORD
>- **elliptical reference**: FIRST/ FIRST OF EMPLOYEE-NAME / FIRST OF EMPLOYEE-RECORD

## 레코드 필드의 구현

- 레코드 필드들은 인접된 메모리 위치들에 저장됨
- 오프셋 주소: 레코드의 시작 주소에 상대적이며, 필드 접근들은 모두 이러한 오프셋을 사용하여 처리됨
- 오프셋을 가지면 메모리가 어디에 배정되든 쉽게 찾을 수 있다

# 공용체(union) 타입

- 그 변수가 프로그램 실행 중 다른 시기에 다른 타입의 값을 저장할 수 있는 타입
- struct는 갖고있는 타입별로 자리가 할당되지만, union은 갖고있는 타입 중 가장 큰 타입만큼만 할당됨

## 판별(discriminated) 공용체와 자유(free) 공용체

### 자유 공용체

- Fortran(equivalence), C, C++(union)
- 프로그래머는 그 사용에 있어서 타입 검사로부터 완전한 자유가 허용됨
- 한마디로 type checking 안함

### 판별 공용체

- ALGOL 68, Ada
- 각 공용체 구조가 타입 지시자를 포함함
- type checking 함

# 리스트(list) 타입

- Scheme과 Common LISP의 리스트는 괄호로 구분되고, 원소들은 어떤 구분자도 구분되지 않음
> e.g. (A B C D)
- Python의 리스트는 배열로서도 역할함
  - 변경 가능함(mutable)
  - 어떤 데이터 값이나 객체도 포함 가능
> e.g. myList = [3, 5, 8, 'apple']

# 튜플(tuple) 타입

- 튜플은 **원소들이 명명되지 않는다**는 것을 제외하면 레코드와 유사함
- 변경 불가(immutable)
- 튜플이 변경될 필요가 있으면 list 함수를 사용해 배열로 변환할 수 있다(python)
> in python<br/>
myTuple = (3, 5.8, 'apple')<br/>
print(myTuple[1]) -> 5.8<br/>
myTuple[1] = 10 -> X

# 포인터 타입과 참조 타입

- 포인터 타입은 그 변수가 메모리 주소와 특수 값 nil(null)로 구성되는 값들의 범위를 갖는 타입
#### 포인터의 두 가지 용도
1. 포인터는 간접 주소지정의 어떤 능력을 제공
2. 포인터는 동적 기억공간을 관리하는 한 가지 방식을 제공
  - 포인터는 동적으로 할당되는 **힙**이라 불리는 기억공간 영역의 한 위치 접근에 사용될 수 있다 

<br/>
- **힙-동적 변수**: 힙으로부터 동적으로 할당되는 변수
  - 단지 포인터나 참조 타입 변수들에 의해서만 참조 가능
- **무명 변수**: 이름이 없는 변수들

to be continued...




<br/><br/><br/>
**참고 문헌**<br/>
Concepts of Programming Languages, Robert W. Sebesta -10th ed.<br/>
위키백과, https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%88%EC%BD%94%EB%93%9C
