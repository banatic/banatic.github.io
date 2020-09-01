---
layout: default
title: 4장 레지스터 전송과 마이크로 연산
nav_order: 4
parent: Mano의 컴퓨터시스템구조
grand_parent: 컴퓨터시스템구조
use_math: true
last_modified_date: 2020-08-29T07:18:08+0900
---

# **레지스터 전송과 마이크로 연산**
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# 레지스터 전송 언어

레지스터에 저장된 데이터를 가지고 실행되는 동작을 **마이크로 연산(micro-operation)**이라고 한다.

하나의 클럭 펄스 동안에 실행되는 기본적인 동작이다.

레지스터간의 마이크로 연산 전송을 보다 간단하게 표현하기 위해 사용하는 기호들을 **레지스터 전송 언어(register transfer language)**라고 한다.

# 레지스터 전송

레지스터는 머리글자들을 대문자로 표시한다.

실제로 사용되는 레지스터들의 종류는 5단원에서 다루게 될 것이다.

n비트 레지스터들의 각 플립플롭들은 맨 오른쪽의 것을 0으로 하여 n-1까지 번호가 매겨지게 된다.

그 중 특정 비트를 표현하기 위해서는 괄호를 이용한다. 상위 바이트와 하위 바이트를 또한 H, L로 표현하기도 한다. ex) R1(0-7) = R1(L), R1(8-15) = R1(R)

## 레지스터 전송의 표현

레지스터 사이의 전송은 치환(replacement) 연산자를 이용하여 다음과 같이 나타낸다.

$ R2 \leftarrow R1 $

제어 조건(P)에 따른 레지스터 전송은 다음과 같이 표현할 수 있다.

$ If(P=1) then(R2 \leftarrow R1) $

$ P:R2 \leftarrow R1 $

두 가지가 같은 표현이다
{: .text-grey-dk-000 .fs-3 } 

또한 동시에 여러 개의 전송이 일어날 수 있는데, 다음은 T = 1일 때 두 레지스터의 내용이 교체되는 것을 의미한다.

$ P:R2 \leftarrow R1, R1 \leftarrow R2  $

## 메모리 전송의 표현

메모리 워드로부터 외부 세계로의 전송은 읽기(read) 동작을, 메모리에 새로운 정보를 저장하는 것은 쓰기(write) 동작에 의해 이루어진다.

메모리 워드는 M으로 나타내고, 주소는 M 다음의 각괄호 안에 표시하게 된다.

예시로, 메모리의 주소를 주소 레지스터(address register, AR)로부터 받고 데이터 레지스터(data register, DR)에 전송하는 읽기 동작은 다음과 같이 표기한다.

$ READ:DR \leftarrow M[AR] $

## 전송 타이밍

![transfer_block](../pic/2/transfer_block.png)

위와 같은 블럭도로 $ P:R1 \leftarrow R2 $ n비트 전송이 이루어진다고 가정하자.

![transfer_timing](../pic/2/transfer_timing.png)

P는 시간 t에서 클럭 펄스의 상승 모서리와 동기되어 시작되고, t+1에서 전송을 마치기 위해 0으로 되돌아 온다.

**P가 t에서 활성화되었지만 실제 전송은 t+1에서 클럭의 상승변이가 일어날 때 까지 발생하지 않음을 유의해야 한다.**

## 버스를 이용한 전송

모든 레지스터들이 네트워크의 그물형(mesh type)마냥 독립된 전송 라인을 가지게 된다면 숫자가 너무 많아지게 된다.
 
따라서 **버스(bus)**라는 공유되는 전송라인을 사용하게 되는데, 이 때 대상 레지스터에만 데이터를 전송하기 위해 선택 입력이 필요하게 된다.

### 멀티플렉서를 이용한 버스
선택 입력에 따른 출력을 하기 위해 멀티플렉서(MUX)를 이용하여 BUS를 구성하게 되는데, 기본적인 형태는 각각의 멀티플렉서에 레지스터들의 똑같은 번호 입력들이 들어가는 형태이다.

![bus_3d](../pic/2/bus_3d.png)

원래 책에서는 평면 블록도인데 그리기 힘들어서 3d로 겹쳐봤다..
{: .text-grey-dk-000 .fs-3 } 

위는 4라인 공통버스의 모습이다. 

각각의 레지스터들은 색으로 구분지어놨고, selection에 따라서 output의 색을 정한다고 생각하면 된다.

위 그림을 보면 레지스터의 비트 개수(빨간 레지스터 4bit = 파란 레지스터 4bit ...)만큼의 MUX가 필요하고, 또한 그 입력은 레지스터의 갯수(빨강, 노랑, 초록, 파랑)만큼의 입력을 가져야함을 알 수 있다.

정리하자면 **n비트의 k개 레지스터를 멀티플렉스하여 n 라인의 공통 버스를 만드는 버스시스템에서는 n개의 k*1 멀티플렉서**가 필요하게 된다.

### 3-상태 게이트를 이용한 버스

MUX 대신 3-상태 게이트를 이용하여 구성할 수도 있다.

3-상태 게이트에서 두 개의 상태는 일반적인 게이트와 같지만, 세 번째 상태는 **고저항 상태(high-impedance state)**이다. 개회로와 같은 상태로 생각하면 된다.

대상 레지스터 이외의 레지스터의 출력을 고저항 상태로 만든다면 버스 시스템을 구축할 수 있게 된다.

이 때 대상 레지스터를 제외한 레지스터들의 출력을 고저항 상태로 만들기 위해 디코더를 이용하게 된다.

MUX에 비해 로딩 효과(loading effect)가 없다는 이점이 있다.

### 버스 전송에서의 표현

버스 전송시에 기호표현은 다음과 같다.

$ BUS \leftarrow C, R1 \leftarrow BUS $

그러나 버스가 시스템에 존재한다고 가정한다면 생략할 수 있다.

$ R1 \leftarrow C $

하지만 설계자는 버스를 이용하는 것을 염두에 두어야 한다. 

후의 단원에서도 전송이 버스를 이용하는지 파악하는 것이 중요하다.

# 마이크로 연산

마이크로 연산은 레지스터에 저장된 데이터에 대해 수행되는 기본적인 연산이며, 흔히 네 가지로 분류할 수 있다.

1. 레지스터 사이에서 이진 정보를 전송하는 **레지스터 전송 마이크로 연산**
2. 레지스터에 저장된 수치 데이터에 대해 산술 연산을 수행하는 **산술 마이크로 연산**
3. 레지스터에 저장된 비수치 데이터에 대해 비트 조작 연산을 수행하는 **논리 마이크로 연산**
4. 레지스터에 저장된 데이터에 대해 시프트 연산을 수행하는 **시프트 마이크로 연산**

## 레지스터 전송 마이크로 연산

위에서 충분히 다뤘다고 생각하고 다루지 않는다.

## 산술 마이크로 연산

연산에는 덧셈, 뺄셈, 인크리멘트, 디크리멘트, 시프트 등이 있고 다음과 같이 표기할 수 있다.

$ R3 \leftarrow R1 + R2 $

또한 뺄셈은 다음과 같이 표기할 수 있다.

$ R3 \leftarrow R1 - R2 $

$ R3 \leftarrow R1 + \overline{R2} + 1 $ (보수를 이용한 뺄셈)

곱셈과 덧셈은 조합 회로로 구현되었을 때에만 마이크로 연산으로 간주한다.
{: .text-grey-dk-000 .fs-3 } 

## 논리 마이크로 연산

부울대수에서와 같이 AND, OR, XOR 등등을 지원한다고 생각하면 된다.

예시만 몇 가지 들고 넘어가도록 한다.

| Boolean function | Microoperation | Name |
|:--|:--|:--|
| $F_{0}$ | $F \leftarrow 0$ | Clear |
| $F_{1}$ | $F \leftarrow \overline{A \vee B}$| NOR |
| $F_{2}$ | $F \leftarrow all\ 1's $ | set to all 1's |

## 시프트 마이크로 연산

**시프트 마이크로 연산(shift microoperation)**은 레지스터의 내용을 왼쪽 및 오른쪽으로 시프트하는 연산이다.

시프트 연산에는 3가지가 존재한다.

1. 직렬 입력으로 0이 전송되는 **논리 시프트(logical shift)**
2. 직렬 출력을 직렬 입력에 연결하여 정보의 손실이 일어나지 않는 **순환 시프트(circular shift or rotate shift)**
3. 부호가 있는 수를 시프트할 때 최상위비트를 고려하는 **산술 시프트(arithmetic shift)**

| Symbolic designation | Name | if applyed to '12345'?|
|:--|:--|
| $R \leftarrow shl\,R$ | Shift-left register $R$ | 12340 |
| $R \leftarrow shr\,R$ | Shift-right register $R$ | 01234 |
| $R \leftarrow cil\,R$ | Circular shift-left register $R$ | 23451 |
| $R \leftarrow cir\,R$ | Circular shift-right register $R$ | 51234 |
| $R \leftarrow ashl\,R$ | Arithmetic shift-left register $R$ | 13450 |
| $R \leftarrow ashr\,R$ | Arithmetic shift-right register $R$ | 10234 |



# 마이크로 연산을 위한 하드웨어

## 산술 연산을 위한 회로

### 이진 가산기

두 이진수에 대한 덧셈을 수행하기 위해 전가산기(full adder)를 이어붙인 회로를 **이진 가산기(binary adder)**라고 한다.

블록도는 다음과 같다.

![binary_adder](../pic/2/binary_adder.png)

### 이진 가감산기

뺄셈은 2의 보수를 이용한 덧셈으로 계산되기 때문에 전가산기에 exclusive-OR 게이트를 추가하면 뺄셈도 구현할 수 있다.

밑 블록도의 회로는 모드 입력 M이 0이면 가산기, 1이면 감산기로 동작한다.

![binary_addsuber](../pic/2/binary_addsuber.png)

### 이진 인크리멘터

반가산기(half adder)를 직렬로 연결한 회로를 **이진 인크리멘터(binary incrementer)**라고 한다.

블록도는 다음과 같고, 최하위 비트에 해당하는 반가산기의 입력이 1이기 때문에 인크리멘트 연산을 수행할 수 있다는 것을 확인하자.

![binary_incre](../pic/2/binary_incre.png)

### 산술 회로

![arith_circuit](../pic/2/arith_circuit.png)

위 회로들을 모두 구현한 하나의 회로이다. 위 회로는 선택 입력에 따라 7가지의 연산을 구현할 수 있다.

함수표는 다음과 같다.

<div class="truth-table" markdown="1">

| $S_{1}$ | $S_{1}$ | $C_{in}$ | Y | $D = A + Y + C_{in}$ | Microoperation |
|:--|:--|:--|:--|:--------|:----| 
| 0 | 0 | 0 | B | $D=A+B$ | Add |
| 0 | 0 | 1 | B | $D=A+B+1$ | Add with carry |
| 0 | 1 | 0 | B | $D=A+\overline{B}$ | Substract with borrow |
| 0 | 1 | 1 | B | $D=A+\overline{B}+1$ | Substract |
| 1 | 0 | 0 | B | $D=A$ | Transfer A |
| 1 | 0 | 1 | B | $D=A+1$ | Increment A |
| 1 | 1 | 0 | B | $D=A-1$ | Decrement A |
| 1 | 1 | 1 | B | $D=A$ | Transfer A |

</div>

외울 필요는 없다
{: .text-grey-dk-000 .fs-3 } 

## 시프트를 위한 회로

2단원에 나오듯 플립플롭을 이용하여 시프트 하드웨어를 구현할 수 있지만, 펄스가 필요하다는 것은 큰 단점이다.

따라서 많은 레지스터를 가진 프로세서는 MUX를 이용하여 하드웨어를 구현한다.

![shift](../pic/2/shift.png)

두 개의 직렬 입력은 시프트의 종류를 선택하기 위해 다른 멀티플렉서로 제어될 수 있을 것이다.

## 산술 논리 시프트 장치

흔히 ALU(Arithmetic logic unit)이라고 불리는 산술논리 + 시프트 회로이다.

![arith_logic_shift](../pic/2/arith_logic_shift.png)

