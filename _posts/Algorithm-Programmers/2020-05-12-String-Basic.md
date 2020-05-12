---
layout: post
title: 프로그래머스 Level 1 문자열 다루기 기본 (Python)
comments: true
categories: [Algorithm/Programmers]
tags: [Python, Algorithm, Coding]
---

프로그래머스의 코딩테스트 연습문제 중 [문자열 다루기 기본](https://programmers.co.kr/learn/courses/30/lessons/12918) 문제의 정답.
<br><br>

<u> Python 코드</u>
<br>

```python

def solution(s):
    letter = "abcdefghijklmnopqrstuvwxyz"
    for i in range(len(s)):
      # 문자열 's'에 알파벳이 있으면 False 반환
      if s[i] in letter:
        return False
    # 위의 경우가 아닐 시, 's'의 길이가 4 혹은 6인가에 대한 Boolean 값 반환
    return len(s) == 4 or len(s) == 6

```
<br>
더 깔끔하게 한줄로 끝낼 수도 있을 것 같았다. <br>
그리고 내 예상은 맞았다.
<br>
<br>
## 다른 사람의 코드
<br>
```python

def alpha_string46(s):
    return s.isdigit() and len(s) in (4, 6)

```
<br>
.isdigit() 이라는 함수가 있었구나...
그리고 len(s)의 값이 (4, 6)에 있는지 확인하는 부분도 깔끔했다.
<br><br>
다른 사람의 코드를 보면서 배우는 것도 많은 도움이 되는 것 같다.<br>
나도 나중엔 다른사람이 내 코드를 보며 배울 점을 찾게되는 순간이 오길..
<br>
