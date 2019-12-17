---
layout: post
title: 프로그래머스 Level 1 문자열 내 P와 Y의 개수 (Python)
comments: true
categories: [Algorithm/Programmers]
tags: [Python, Algorithm, Coding]
---


프로그래머스의 코딩테스트 연습문제 중 [문자열 내 P와 Y의 개수](https://programmers.co.kr/learn/courses/30/lessons/12916) 문제의 정답입니다.
<br>
<br>

<u>코드는 Python3 로 작성되었습니다.</u>

<br>
<br>

```python
def solution(s):
    answer = True              
    p = s.lower().count('p')    # 문자열 내 모든 문자를 소문자 (대문자도 가능) 로 변환한 후, count function으로 'p'의 개수 계산 후 값 저장  
    y = s.lower().count('y')    # Y도 같은 방식으로 저장

    if p == y:                  # p와 y의 개수가 같다면, 그대로 return answer
        return answer
    if p == 0 and y == 0:       # p와 y가 모두 하나도 없는경우, return answer
        return answer
    if p != y:                  # p와 y의 개수가 다르다면 answer = False가 되고 return answer.
        answer = False
        return answer
```

<br><br>

레벨 1인만큼 정말 쉬운 것 같아요. 얼른 더 높은 레벨도 쉬운 날이 올 수 있도록 더 많이 풀어보고 노력해야겠어요! :)
<br><br>
감사합니다!
