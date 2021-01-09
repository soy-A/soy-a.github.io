---
layout: post
title: "[프로그래밍 언어론] 구문과 의미론 - 구문"
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

# 구문 기술
- 문장(sentence): 알파벳 문자들로 구성된 문자열
- 언어(language): 문장의 집합
- **어휘항목**(lexeme): 언어의 가장 작은 구문 단위
> e.g. 변수 이름, 연산자, 특수어
- **토큰**(token): 어휘항목들의 부류(category)
> e.g. 식별자

- int a;
 - 어휘항목: int, a, ;
 - 토큰: "int" -> 타입, "a" -> 식별자, ";" -> 세미콜론

---

## 언어 인식기와 언어 생성기

#### 언어 인식기
- 입력 문자열을 읽고 주어진 프로그램이 언어에 속하는지를 판단한다

#### 언어 생성기
- 언어의 문장들을 생성하는 데 사용되는 장치이다
- 특정 문장의 구조를 생성기가 만들어낸 문장의 구조와 비교하여 올바른지를 결정할 수 있다

---

## 구문 기술의 형식적 방법

- **Backus-Naur form** (BNF): 프로그래밍 언어 기술에 가장 널리 사용된다
-  **확장 BNF** (EBNF): BNF보다 readability와 writability가 향상된다
-  BNF는 문맥 자유 문법(context-free grammars)와 거의 동일하다

### Backus-Naur 형식 (BNF)
- **메타언어**(meta-language): 다른 언어를 기술하는 데 사용되는 언어
- BNF는 프로그래밍 언어를 위한 메타언어이다
- BNF는 구문 구조에 대해서 **추상화**를 사용한다

#### BNF의 기본 원리
- **LHS**(left-hand side): 화살표 왼쪽에 위치한 텍스트로, 정의되고 있는 추상화이다
- **RHS**(right-hand side): 화살표 오른쪽에 위치한 텍스트로, 토큰, 어휘항목, 다른 추상화에 대한 참조 등으로 구성된다
- **non-terminals**(non-terminal symbols): BNF에서의 추상화
- **terminals**(terminal symbols): 규칙에 포함된 어휘항목과 토큰
- **문법**: 규칙들의 모임
> e.g. Java의 if문<br/>
\<if_stmt\> -> if (\<logic_expr\>) \<stmt\>	<br/>
                   | if (\<logic_expr\>) \<stmt\> else \<stmt\>	<br/>
 # \<stmt\>는 단일 문장이나 복합문을 나타낸다<br/>
 # |는 여러 정의가 한 개의 규칙으로 작성될 수 있게 한다(OR의 역할)

#### BNF 규칙
- 규칙은 **LHS**(left-hand side), **RHS**(right-hand side)을 가지며, **terminal**, **non-terminal** 기호들로 이루어져있다
- 문법은 규칙들의 유한집합이다
- 추상화(또는 non-terminal 기호)는 한 개 이상의 RHS를 갖는다

#### 리스트 명세
- 구문 요소들의 리스트를 기술하기 위해 **재귀**(recursion)가 사용된다
- 규칙에서 LHS가 RHS상에 나타나면 그 규칙은 재귀적(recursive)이다
> \<ident_list\> -> ident<br/>
                      | ident, \<ident_list\>

#### 문법과 유도
> 문법<br/>
\<program\> -> begin \<stmt_list\> end<br/>
\<stmt_list\> -> \<stmt\><br/>
                     | \<stmt\> ; \<stmt_list\><br/>
\<stmt\> -> \<var\> -> A | B | C<br/>
\<expr\> -> \<var\> + \<var\><br/>
                | \<var\> - \<var\><br/>
                | \<var\><br/>
                  
- **유도**(derivation, ⇒)는 시작 기호(특정 non-terminal기호)로부터 시작되고 문장(모든 terminal기호)으로 끝나는 **일련의 규칙 적용**을 의미한다
- 유도과정에서의 각 문자열을 문장 형태라고 부른다
- non-terminal을 포함하지 않고 terminal, 또는 어휘항목만으로 구성된 문장 형태가 **생성된 문장**(generated sentence)이다
- **최좌단 유도**(leftmost derivation)는 각 문장 형태에서 가장 왼쪽에 위치한 non-terminal 이 대체되는 순서를 사용하는 유도이다
- 유도는 최좌단이나 최우단도 아닌 순서일 수 있다
- 한마디로 계속 치환하는 것, Parse tree로 표현 가능하다
> 유도<br/>
\<program\> ⇒ begin \<stmt_list\> end<br/>
                   ⇒ begin \<stmt\> end<br/>
                   ⇒ begin \<var\> = \<expr\> end<br/>
                   ⇒ begin A = \<expr\> end<br/>
                   ⇒ begin A = \<var\> + \<var\> end<br/>
                   ⇒ begin A = B + \<var\> end<br/>
                   ⇒ begin A = B + C end<br/>
            
#### 파스 트리(parse tree)

- 유도 과정을 **계층적 구조**로 나타낸 것
> 위의 예시를 파스트리로 나타내면 다음과 같다<br/>
<img width="428" alt="스크린샷 2021-01-09 오후 8 30 10" src="https://user-images.githubusercontent.com/63772786/104090354-8fcdf900-52b9-11eb-9f96-b137d96b6b38.png">

#### 문법의 모호성

- 같은 문법을 바탕으로 생성된 문장에서 서로 다른 **파스 트리가 여럿 생성됨** -> **모호하다**
> 다음 규칙을 바탕으로 한 문장(const - const / const)는 두 개의 파스트리를 갖는다<br/>
\<expr\> -> \<expr\> \<op> \<expr\> | const<br/>
    \<op\> -> / | -<br/>
<img width="856" alt="스크린샷 2021-01-09 오후 8 50 16" src="https://user-images.githubusercontent.com/63772786/104090764-492dce00-52bc-11eb-98ee-4500b2f6358b.png">

#### 모호성을 없애는 방법 - 연산자 우선순위

- 파스트리로 **연산자 우선순위**를 표시해주면 모호성이 사라진다
> e.g. 다음과 같이 연산자의 순서를 규칙에서 정해준다<br/>
\<expr\> -> \<expr\> - \<term\> \| \<term\><br/>
\<term\> -> \<term\> / const \| const

#### 모호성을 없애는 방법 - 연산자 결합 규칙

- 문법으로 **연산자 결합 규칙**을 나타내주는 방법으로도 모호성 문제를 해결할 수 있다
> e.g.<br/>
\<expr\> -> \<expr\> + \<expr\> | const (모호하다)<br/>
\<expr\> -> \<expr\> + const | const (모호하지 않다)

---

## 확장 BNF (EBNF)

- [], {}, ()는 **메타 기호**로, 표기하는 역할을 할 뿐 구문 요소에 속하는 터미널 기호가 아니다
- **선택적인 부분** 표기는 **대괄호[]** 안에 이루어진다
> EBNF: \<if-stmt\> -> **if** (\<expr\>) \<stmt\> [**else** \<stmt\>]<br/>
BNF: \<if-stmt\> -> **if**(\<expr\>) \<stmt\><br/>
                           | **if** (\<expr\>) \<stmt\> **else** \<stmt\>
- **다중 선택 사항**의 경우 **소괄호()** 안에 대상을 포함시키고, 이들을 **OR 연산자 |**으로 구분한다
> EBNF: \<term\> -> \<term\> ( + \| - ) const<br/>
BNF:  \<term\> -> \<term\> + const<br/>
                       | \<term\> - const
- 무한정 **반복**되거나 **생략**할 수 있는 경우는 **중괄호{}**안에 위치시킨다
> \<ident\> -> letter {letter \| digit}
- BNF 규칙 \<expr\> -> \<expr\> + \<term\>에서 +연산자는 좌결합적
- EBNF 규칙 \<expr\> -> \<term\> {+ \<term\>}은 결합 규칙의 방향을 암시하지 않는다
> 구문 분석기가 처리함

<br/><br/>

# 속성 문법

- context-free 문법의 확장
- **BNF로 기술하기 어려운 특성**들이 존재한다
> e.g. Java에서 부동-소수점 수의 값은 int 타입의 변수에 배정될 수 없지만, 그 반대는 가능하다. 이러한 제한사항을 모두 BNF로 명세한다면 문법이 너무 커지게 된다.
- **정적 의미론** 규칙을 기술
- 컴파일러 설계(정적 의미론 검사)
> 정적 의미론(static semantics) -> 실행 전 오류 여부 파악 가능<br/>
동적 의미론(dynamic semantics) -> 실행해야 파악 가능

---

## 속성 문법의 정의

- 각 문법 기호 X에 속성들의 집합 A(X)가 연관된다
- 각 문법 규칙은 non-terminal의 특정 속성을 정의하는 함수의 집합을 갖는다
- 각 문법 규칙은 기호들의 속성에 대한 술어 함수(공집합일 수 있다)들의 집합을 갖는다

<br/><br/><br/>
**참고 문헌**<br/>
Concepts of Programming Languages, Robert W. Sebesta -10th ed.