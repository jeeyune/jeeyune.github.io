---
layout: post
title: "[C언어 기초] C언어 동적 할당"
comments: true
categories: [Programming/C]
tags: [C, Memory, Data Structures]
---

이번 포스팅은 C언어의 '동적 할당'에 대해서 써보려고 합니다.   
<br>
[저번 포스팅](https://jeeyune.github.io/programming/c/2019/12/20/C-Memory-Stucture.html)에서 다룬 C언어의 메모리 구조 중 '힙 영역'에 해당하는 부분인데요, 데이터 영역과 스택 영역에 할당되는 메모리의 크기는 *컴파일 중* 에 결정되지만, 힙 영역에 할당되는 메모리의 크기는 프로그램이 실행되는 **런타임** 중에 프로그래머가 직접 결정합니다. 이렇게 프로그래머가 런타임에 메모리를 할당하는 것을 **동적 할당 (Dynamic Allocation)** 한다 라고 합니다.

<br>
<br>

**힙 영역이 필요한 이유?**

<br>

1. 데이터 영역 또는 스택 영역에 저장되는 변수로 짜기 힘든 코드를 작성 가능.
<br>
2. 메모리를 낭비하지 않을 수 있다.
<br>
3. 프로그래머가 필요한 만큼, 원하는 만큼 메모리를 할당할 때 적당하다.

<br><br>

**동적 할당 방법**
<br><br>

# <span style="color:SeaGreen"> 1. malloc() 함수 </span>

malloc() 함수는 동적으로 메모리를 할당하는 함수로, 프로그램이 실행 중일 때 사용자가 직접 힙 영역에 메모리를 할당하도록 도와주는 함수이다. <br>

*malloc() 함수의 원형*

```c
#include <stdio.h>

void *malloc(size_t size)    //size_t == 부호 없는 정수
```
<br>
malloc() 함수는 할당받는 메모리의 크기를 바이트 단위로 전달받는다. 그리고나서 아직 할당되지 않고 크기에 맞는 적당한 블록을 찾아 할당 한 뒤, 그 블록의 첫 번째 바이트를 가리키는 **주소** 를 반환한다. 왜냐하면 malloc()함수는 메모리를 할당만 하는 함수이기 때문에 프로그래머가 어떤 데이터 형을 저장하는지 알 수 없다. 예를 들어서, 4바이트를 할당했을때, 그것이 int형인지, float형인지 알 수 없기 때문에 void 포인터를 리턴해 프로그래머가 필요한 용도로 변환할 수 있도록 한 것이다.  즉, malloc()함수에 접근하기 위해서는 포인터를 사용해야 한다. 만약 int형 데이터를 저장해야 한다면 void* 를 int*로 변환해야 한다. <br>

```c
int *i = (int*) malloc(sizeof(int))   
//malloc(sizeof(int)) --> 4바이트 할당, (
//int*) --> void* 형을 int* 형으로 변환
// 다른 형들도 같은 방식으로 변환
```
<br>

주소를 통해 변환하기 때문에 변수의 메모리 크기가 달라지더라도 주소는 동일하다. 만약 적당한 블록을 찾지 못했을 경우 (메모리 할당에 실패했을 경우)엔 null을 반환한다.
<br><br>

*예시*
<br>

```c
#include <stdio.h>

int main(){
  int arr[10];          //배열
  int * arr_ptr;        //포인터

  for (int i = 1; i <= 10; i++){
    arr[i] = i + 1;     // 값 대입    
  }

  arr_ptr = (int*) malloc(sizeof(int) * 10);  // 배열 크기만큼 메모리 할당

  char* n = (char*) malloc(16);      // char는 1바이트, 총 16개의 변수 생성
  int* n = (int*) malloc(16);        // int는 4바이트, 총 4개의 변수 생성
  double* n = (double*) malloc(16);  // double은 8바이트, 총 2개의 변수 생성
}
```
<br>

# <span style="color:SeaGreen"> 2. free() 함수 </span>

free()함수는 할당받은 메모리 공간을 다시 운영체제로 반환, 즉 소멸해주는 함수이다. 동적 할당으로인해 힙 영역에 할당된 메모리의 크기는 런타임 내내 바뀌기 때문에 사용이 끝난 메모리를 반환해주지 않으면 메모리가 부족해 질 수 있다. 이런 현상을 메모리 누수 (Memory Leak) 라고 한다. 그러므로 반드시 free()함수를 사용해 메모리를 반환해 주어야한다.

<br>

*free() 함수의 원형*


```c
#include <stdio.h>

void free(void *ptr);
```
<br>

free()함수는 반환하려는 메모리의 포인터, 즉 주소를 전달받는다. void형 포인터이기 때문에 어떠한 타입의 포인터라도 전달이 가능하다.
<br><br>

*예시*

```c
#include <stdio.h>

int main(){
  int arr[10];          //배열
  int * arr_ptr;        //포인터

  for (int i = 1; i <= 10; i++){
    arr[i] = i + 1;     // 값 대입    
  }

  arr_ptr = (int*) malloc(sizeof(int) * 10);  // 배열 크기만큼 메모리 할당

  free(arr_ptr);        // 동적 할당된 메모리 반환
}
```
<br>

# <span style="color:SeaGreen"> 3. calloc() 함수 </span>

calloc()함수는 malloc()함수와 흡사한 역할을 하는 함수지만, 다른 점이 있다면 할당하려는 메모리의 크기를 두개의 인수로 나누어 전달받는 점, 그리고 할당받은 후 해당 메모리의 모든 비트 값을 0으로 초기화 한다는 점이다.
<br>

- malloc 은 할당된 공간의 값을 바꾸지 않는다
- calloc 은 할당된 공간의 값을 모두 0으로 바꾼다

<br>

*calloc()함수의 원형*


```c
#include <stdio.h>

void *calloc(size_t count, size_t size);  
// size 크기의 변수를 count 개 만큼 저장할 수 있는 공간을 할당하라는 뜻


arr1 = (int*) malloc(len_arr * sizeof(int));     // arr1 == arr2
arr2 = (int*) calloc(len_arr, sizeof(int));
```
<br>

# <span style="color:SeaGreen"> 3. realloc() 함수 </span>

realloc()함수는 이미 할당된 메모리의 크기를 변경해 재할당할 때 사용하는 함수이다.
<br>
*realloc()함수의 원형*
<br>
```c
#include <stdio.h>

void *realloc(void *ptr, size_t size);
```
<br>

이미 할당한 변수의 주소, 즉 포인터를 ptr에 넣고, 해당 공간에 재할당할 크기를 size에 대입한다.
<br>

```c
arr = (int*) malloc(len_arr * sizeof(int));   //동적 할당
new_len_arr = len_arr + added_len
arr = (int*) realloc(*arr, (new_len_arr * sizeof(int))); //메모리 추가할당
```
<br>

만약 기존 메모리 위치에 공간이 충분히 있다면 바로 이어서 공간을 할당하고, 그렇지 않으 경우엔 다른 공간에 기존 데이터를 복사한 후 이어서 추가 메모리 공간을 할당한다.

<br><br><br>

자세히 설명하려다 보니 글이 좀 길어진 것 같은데, 도움이 되었으면 좋겠네요!


혹시나 위의 내용 중 개선사항, 또는 틀린 내용이 있다면 댓글로 남겨주세요!

<br>

감사합니다 :)
<br>
