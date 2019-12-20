---
layout: post
title: "[C언어 기초] C언어 메모리 구조"
comments: true
categories: [Programming/C]
tags: [C, Memory, Data Structures]
---

지난 포스팅에서 얘기했듯이, 이번 포스팅은 C언의 메모리 구조에 대해서 써보려고 합니다.   
<br>
C언어를 제대로 이해하고 효율적으로 사용하기 위해서는 메모리 구조를 잘 알고 있어야해요. 다른 언어도 마찬가지라고 생각합니다.
<br>
<br>

**C언어의 메모리 구조**

<br>
C언어의 메모리 구조는 크게 4가지 영역으로 나눌 수 있습니다.
<br><br>
![cmemory.PNG](/assets/img/cmemory.PNG)
<br>
[이미지 출처](http://tcpschool.com/c/c_memory_structure)
<br>
1. 코드 영역 (Code Area)
2. 데이터 영역 (Data Area)
3. 힙 영역 (Heap Area)
4. 스택 영역 (Stack Area)
<br>
<br>

# <span style="color:SeaGreen"> 1. 코드 영역 (Code Area) </span>

메모리의 *'코드 영역'* 은 실행되는 프로그램의 코드가 저장되는 메모리 공간이다. *'텍스트 영역'* 이라고도 부르며, C언어를 통해 작성한 함수와 명령어들이 저장되는 공간. CPU가 코드영역에 저장돤 명령어를 하나씩 처리한다.
<br><br>

# <span style="color:SeaGreen"> 2. 데이터 영역 (Data Area) </span>
*데이터 영역* 은 프로그램의 전역 변수(Global Variable)와 정적 변수(Static Variable)가 저장되는 영역이다. 메인 함수가 불러와지기 전에 데이터 영역에 할당되기 때문에 프로그램이 시작됨과 동시에 메모리가 할당되며, 프로그램이 종료되면 자동으로 소멸한다. 프로그램이 종료되지 않으면, 사라지지 않고 남아있게 된다.
<br><br>

```c
#include <stdio.h>

int a = 5;    // 데이터 영역
int b = 10;   // 데이터 영역

int main(){
  ...
}
```
<br><br>

# <span style="color:SeaGreen"> 3. 힙 영역 (Heap Area) </span>
*힙 영역* 은 프로그래머가 메모리를 할당하고 소멸시킬 수 있는 변수들이 할당되는 영역이다. 이 영역은 할당해야 할 메모리의 크기를 프로그램이 실행되는 동안, 즉 런타임에 결정해야 하는 경우에 유용하게 사용될 수 있다. 힙 영역을 사용하기 위해서는 **동적 메모리 할당** 에 대해서 공부해야 하는데, 다음 포스팅에 자세하게 다룰 내용이다.
<br><br>

# <span style="color:SeaGreen"> 4. 스택 영역 (Stack Area) </span>
*스택 영역* 은 지역 변수(Local Variable)와 매개 변수(Parameter)가 저장되는 메모리 공간으로 컴파일하는 동안에 크기를 결정하게 된다. 함수 안에서 선언된 변수들로, *프로그램이 아닌* **함수** 가 종료될 때 저장되어 있던 메모리값이 소멸됨.
<br><br>


*예시 코드*



```c
#include <stdio.h>

int a = 1;     // 데이터 영역에 할당
int b = 2;     // 데이터 영역에 할당

int main(){
  int c = 10;  // 스택 영역에 할당
}

int function1(int d){    // 매개변수 d -> 스택영역에 할당
  int e = 15;            // 지역변수 e -> 스택영역헤 할당
}
```
<br><br>



혹시나 위의 내용 중 개선사항, 또는 틀린 내용이 있다면 댓글로 남겨주세요!

<br>

감사합니다 :)
<br>
