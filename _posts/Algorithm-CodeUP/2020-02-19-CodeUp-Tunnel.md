---
layout: post
title: 코드업 문제 1164번 - 터 통과하기 1 (C언어)
comments: true
categories: [Algorithm/CodeUp]
tags: [C, Algorithm, Coding]
---

코드업  **1164번** 풀이입니다.

<br>
<u>모든 코드는 C로 작성되었습니다</u>
<br>

# <span style="color:SeaGreen"> # 1164번 </span>
<br>

```c
#include <stdio.h>

int main(){
    int h1, h2, h3;

    scanf("%d%d%d", &h1, &h2, &h3);

    if(h1 <= 170 || h2 <= 170 || h3 <= 170)
      printf("CRASH");

    else
      printf("PASS");

    return 0;

}
```
<br>

감사합니다.
