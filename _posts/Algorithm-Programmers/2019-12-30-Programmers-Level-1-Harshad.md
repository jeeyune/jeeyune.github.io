---
layout: post
title: 프로그래머스 Level 1 하샤드 수 (Python)
comments: true
categories: [Algorithm/Programmers]
tags: [Python, Algorithm, Coding]
---

프로그래머스의 코딩테스트 연습문제 중 [하샤드 수](https://programmers.co.kr/learn/courses/30/lessons/12947) 문제의 정답입니다.
<br><br>

<u> Python 코드</u>
<br>

```python
def solution(n):
    return n % sum([int(c) for c in str(n)]) == 0
```

<br><br>
감사합니다!
