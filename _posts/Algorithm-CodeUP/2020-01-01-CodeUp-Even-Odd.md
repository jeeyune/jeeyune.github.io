---
layout: post
title: 코드업 문제 1161번 - 홀수와 짝수 그리고 더하기 (C언어)
comments: true
categories: [Algorithm/CodeUp]
tags: [C, Algorithm, Coding]
---

코드업  **1161번** 풀이입니다.


<u>모든 코드는 C로 작성되었습니다</u>
<br>

# <span style="color:SeaGreen"> # 1161번 </span>

```c
#include <stdio.h>

int main(){
    int a, b;
    char *a1;
    char *b1;
    char *add;

    scanf("%d%d", &a,&b);

    if (a % 2 == 0) a1 = "짝수";

    else if (a % 2 == 1) a1 = "홀수";


    if (b % 2 == 0) b1 = "짝수";

    else if (b % 2 == 1) b1 = "홀수";


    if ((a + b) % 2 == 0) add = "짝수";

    else if ((a + b) % 2 == 1) add = "홀수";

    printf("%s+%s=%s", a1, b1, add);
}
```
<br><br>

파이썬은 더 간결하게 할 수 있는데, C언어로도 간단하고 간결하게 푸는 법을 더 공부해야 할 것 같아요.
<br><br>

감사합니다.
