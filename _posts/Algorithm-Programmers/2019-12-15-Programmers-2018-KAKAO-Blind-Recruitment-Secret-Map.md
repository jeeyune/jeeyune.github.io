---
layout: post
title: 프로그래머스 2018 카카오 블라인드 채용 [1차] 비밀지도 (Python)
comments: true
categories: [Algorithm/Programmers]
tags: [Python, Algorithm, Coding, Kakao]
---


프로그래머스의 코딩테스트 연습문제 중 [2018 카카오 블라인드 채용 1차 '비밀지도'](https://programmers.co.kr/learn/courses/30/lessons/17681) 문제의 정답입니다.
<br>
<br>

1차 코딩테스트의 첫번째 문제인만큼, 정답률도 81.78%로 높았는데요, 가장 많은 참가언어로는 자바가 전체의 43%, 그 다음이 C++ 36%, 파이썬 11% 등이라고 하네요.
<br>

 1차 코딩 테스트의 합격 기준은 총 7문제 중 **4문제** 이상을 풀이한 분들이라고 합니다.
 <br>

4문제 이상을 풀이한 합격자의 비율은 C++이 25%, 그 다음 파이썬이 24%로 얼마 차이가 나지 않네요! 평균 코드 라인 수도 파이썬이 압도적이라고 합니다. 첫번째 문제는 고작 22줄밖에 안됐다고 해요.


REFERENCE: [2018 카카오 신입 공채 1차 코딩 테스트 문제 해설](https://tech.kakao.com/2017/09/27/kakao-blind-recruitment-round-1/)

<br>

저도 파이썬으로 한번 풀어보았는데, 많은 분들이 저와 비슷하게, 혹은 더 짧은 코드로 풀이하셨던 것 같습니다.
<br>

<u>코드는 Python3 로 작성되었습니다.</u>

<br>
<br>

```python
def solution(n, arr1, arr2):
    answer = []
    for a1, a2 in zip(arr1, arr2):    # arr1과 arr2를 zip()으로 묶기
        a = str(bin(a1 | a2))[2:]     # a1 OR a2를 binary로 바꿔주는 bin() function을 통해 2진수로 바꿔준 후, 불필요한 맨 앞 2자리를 버리기 위해 string으로 변환 후 index slicing
        a = '0' * (n - len(a)) + a    # index slicing을 하게되면, 0으로 시작하는 2진수의 0들이 사라지기 때문에 입력받은 n의 길이에서 숫자만큼의 수를 뺀만큼 '0'을 곱하고 그 숫자를 더해준다.
        a = a.replace('1',"#")        # 1은 #으로 replace
        a = a.replace('0', " ")       # 0은 공백으로 replace
        answer.append(a12)

    return answer
```

<br><br>

이 문제는 비트연산 (Bitwise Operation)에 관한 문제로, if else로도 쉽게 풀 수 있지만, OR과 같은 비트연산을 잘 다룰 수 있는지를 보려고 의도한 것이기 때문에 이런 유형은 비트 연산을 꼭 사용하는 것이 좋을 것 같습니다.
<br><br>
감사합니다!
