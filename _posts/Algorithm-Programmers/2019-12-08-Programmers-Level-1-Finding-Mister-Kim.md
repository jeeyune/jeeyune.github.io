---
layout: post
title: 프로그래머스 Level 1 서울에서 김서방 찾기 정답 (Python)
comments: true
categories: [Algorithm/Programmers]
tags: [Python, Algorithm, Coding]
---


프로그래머스의 코딩테스트 연습문제 중 [서울에서 김서방 찾기](https://programmers.co.kr/learn/courses/30/lessons/12919) 문제의 정답입니다.
<br>
<br>


<u>코드는 Python3 로 작성되었습니다.</u>

<br>
<br>

```python
def solution(seoul):
    kim_loc = seoul.index('Kim')                  # 리스트 seoul에서 Kim의 위치
    answer = "김서방은 {}에 있다".format(kim_loc)  #출력
    return answer
```

<br><br>

감사합니다.
