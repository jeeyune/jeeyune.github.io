---
layout: post
title: 프로그래머스 Level 1 콜라츠 추측 (Python)
comments: true
categories: [Algorithm/Programmers]
tags: [Python, Algorithm, Coding]
---

프로그래머스의 코딩테스트 연습문제 중 [콜라츠 추측](https://programmers.co.kr/learn/courses/30/lessons/42576) 문제의 정답입니다.
<br><br>

<u> Python 코드</u>
<br>

```python
def solution(num):
    count = 0
    while num != 1:              # num이 1이 아닐동안 계속 루프
        if num % 2 == 0:         # 짝수일땐 num을 2로 나눈값으로 초기와
            num = num / 2
            count += 1           # 횟수를 세는 변수에 1씩 추가
            continue

        elif num % 2 == 1:       # 홀수도 마찬가지
            num = num * 3 + 1
            count += 1
            continue

    if count > 500 or num != 1: # 횟수가 500이 넘거나 최종값이 1이 아닐때 -1 반환
        return -1
    elif num == 1:              # 최종값이 1이고 횟수가 500이 넘지 않는 경우, 횟수를 세는 변수 반환
        return count
```
<br>
혹시 더 깔끔하게 해결한 분 있으시면 댓글로 알려주세요!

<br><br>
감사합니다!
