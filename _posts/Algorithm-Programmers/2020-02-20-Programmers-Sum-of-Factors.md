---
layout: post
title: 프로그래머스 Level 1 약수의 합 (C)
comments: true
categories: [Algorithm/Programmers]
tags: [C, Algorithm, Coding]
---

프로그래머스의 코딩테스트 연습문제 중 [약수의 합](https://programmers.co.kr/learn/courses/30/lessons/12928) 문제의 정답입니다.
<br><br>

<u> C 코드</u>
<br>

```c
  #include <stdio.h>
  #include <stdbool.h>
  #include <stdlib.h>

  int solution(int n) {
      int answer = 0;

      for(int i = 1; i <= n; i++){
          if(n % i == 0)
              answer += i;
      }

      return answer;
  }
```

<br><br>
감사합니다!
