---
layout: post
title: 프로그래머스 Level 1 완주하지 못한 선수 (Python)
comments: true
categories: [Algorithm/Programmers]
tags: [Python, Algorithm, Coding]
---


프로그래머스의 코딩테스트 연습문제 중 [완주하지 못한 선수](https://programmers.co.kr/learn/courses/30/lessons/42576) 문제의 정답입니다.
<br>
<br>

<u>코드는 Python3 로 작성되었습니다.</u>

<br>
<br>

```python
def solution(participant, completion):
  participant.sort()      # sort method로 정렬
  completion.sort()

  for i,j in zip(participant, completion):
    if i != j:            # 정렬된 배열 비교 후, 같지 않으면 그 참가자의 이름을 return
      return i
  return participant[-1]  # 완주하지 못한 사람은 한명이라는 전제가 있기에, participant 배열의 마지막 item을 반환합니다.
```

<br><br>
감사합니다!
