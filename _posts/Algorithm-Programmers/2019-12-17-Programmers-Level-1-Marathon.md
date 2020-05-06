---
layout: post
title: 프로그래머스 Level 1 완주하지 못한 선수 (Python, JavaScript)
comments: true
categories: [Algorithm/Programmers]
tags: [Python, JavaScript, Algorithm, Coding]
---


프로그래머스의 코딩테스트 연습문제 중 [완주하지 못한 선수](https://programmers.co.kr/learn/courses/30/lessons/42576) 문제의 정답입니다.
<br>
<br>

<u>코드는 Python 3 와 자바스크립트로 작성되었습니다.</u>

<br>
<br>
[Python]
<br>

```python
def solution(participant, completion):
  participant.sort()      # sort method로 정렬
  completion.sort()

  for i,j in zip(participant, completion):
    if i != j:            # 정렬된 배열 비교 후, 같지 않으면 그 참가자의 이름을 return
      return i
  return participant[-1]  # 완주하지 못한 사람은 한명이라는 전제가 있기에, participant 배열의 마지막 item을 반환.
```
<br>
[JavaScript]
<br>

```javascript
function solution(participant, completion) {
    participant.sort()        // 배열 정렬
    completion.sort()

   for(var i = 0; i < participant.length; i++){
       if(participant[i] != completion[i]){      // 정렬된 배열 비교 후 다른 아이템 리턴
          return participant[i];
       }
   }
}
```
<br>

## 다른 사람의 풀이
<br>
[Python]
<br>
```python
import collections


def solution(participant, completion):
    answer = collections.Counter(participant) - collections.Counter(completion)
    return list(answer.keys())[0]
```
<br>
[JavaScript]
<br>
```javascript
function solution(participant, completion) {
    participant.sort();
    completion.sort();

    for(let i in participant) {
        if(participant[i] !== completion[i]) return participant[i];
    }
}
```
<br>
