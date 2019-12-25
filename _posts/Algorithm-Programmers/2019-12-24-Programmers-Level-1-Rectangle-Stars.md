---
layout: post
title: 프로그래머스 Level 1 직사각형 별찍기 (C, Python)
comments: true
categories: [Algorithm/Programmers]
tags: [C, Python, Algorithm, Coding]
---

프로그래머스의 코딩테스트 연습문제 중 [직사각형 별찍기](https://programmers.co.kr/learn/courses/30/lessons/42576) 문제의 정답입니다.
<br>
<br>

<u> C 버전</u>
<br>

```c
#include <stdio.h>

int main(void) {
    int a, b;
    scanf("%d %d", &a, &b);             
    for(int i = 0; i < b; i++){            
        for(int j = 0; j < a; j++){
            printf("*");
        }
        printf("\n");
    }
}
```


<br><br>

<u> Python 버전</u>
<br>

```python
a, b = map(int, input().strip().split(' '))    #입력값을 받아오는 기본 제공 코드

for i in range(b):     # b = 세로의 길이
    print("*" * a)     # 문자열 곱셈. print 함수에는 기본값으로 end key가 new line character로 되어있어서 줄바꿈을 하지않아도 된다.
```
<br>

요즘 연말에 크리스마스 이브다 뭐다 해서 자꾸 간단한 것들 위주로 포스팅을 하게 되네요ㅠ 곧 좀더 흥미로운 주제로 포스팅 해보도록 노력할게요.
<br>

모두 행복한 연말연시 되세요!

<br><br>
감사합니다!
