---
layout: post
title: "[Easy] Jewels and Stones"
comments: true
categories: [Algorithm/LeetCode]
tags: [Algorithm, Coding, LeetCode]
---


# <span style="color:SeaGreen"> [Easy] Jewels and Stones </span>
<br>

Problem:
<br>
You're given strings J representing the types of stones that are jewels, and S representing the stones you have. Each character in S is a type of stone you have. You want to know how many of the stones you have are also jewels.
<br>
The letter in J are guaranteed distinct, and all characters in J and S are letters. Letters are case sensitive, so "a" is considered a different type of stone from "A"
<br><br>


Example1:
<br>
Input: J = "aA", S = "aAAbbbb"
Output: 3
<br>
Example2:
<br>
Input: J = "z", S = "ZZ"
Output: 0
<br><br>
Note:
- S and J will consist of letters and have length at most 50
- The characters in J are distinct.

<br><br>

해설:<br>
입력값으로 보석 타입이 들어있는 'J' 와 돌 타입이 들어있는 'S' 라는 문자열이 주어진다. 'S' 문자열의 각 문자는 내가 갖고있는 돌이고, 이 돌들 중 얼만큼이 보석도 되는지를 알아내면 된다.  (S = 그냥 돌, J = 돌이지만 보석인 돌)
<br>
J에 있는 문자들은 모두 서로 다른 문자들이고, 같은 문자의 대문자와 소문자는 다른 문자로 간주한다 (a와 A는 서로 다른 문자).
<br>

참고사항:
- S 와 J는 모두 문자로 이루어져있으며 최대 길이는 50이다.
- J 에 있는 문자열은 모두 서로 다른 문자로 이루어져있다.
<br><br>


**Code:**
```python
class Solution:
    def numJewelsInStones(self, J: str, S: str) -> int:
        jewels = list(J)            # 문자열 --> 리스트
        count = 0                   # 갯수 카운트
        for j in range(len(S)):
            for item in jewels:
                if item == S[j]:    # 만약 J의 문자열과 S의 문자열이 같으면 count 변수에 + 1
                    count += 1
                else:               # 같지 않다면, 계속 진행한다
                    continue
        return count                # 더해진 갯수가 들어있는 count 변수를 반환한다.
```  

<br>
