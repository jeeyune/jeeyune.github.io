---
layout: post
title: 프로그래머스 Level 1 가운데 글자 가져오기 (JavaScript)
comments: true
categories: [Algorithm/Programmers]
tags: [JavaScript, Algorithm, Coding]
---

프로그래머스의 코딩테스트 연습문제 중 [가운데 글자 가져오기](https://programmers.co.kr/learn/courses/30/lessons/12903) 문제의 정답.
<br><br>

<u> JavaScript 코드</u>
<br>

```JavaScript

function solution(s) {
    var answer = '';
    if(s.length % 2 === 0){
        answer += s[s.length / 2  - 1]
        answer += s[s.length / 2]
    }
    else{
        answer += s[Math.floor(s.length / 2)]    
    }
    return answer;
}

```
<br>
풀긴 풀었는데 내 코드가 마음에 안들었다.
<br>

## 다른 사람의 코드
<br>

```JavaScript

function solution(s) {
    return s.length % 2 == 0 ? s.substr(s.length / 2 - 1, 2) : s.substr(Math.floor(s.length / 2), 1);
}

```
<br>

삼항연산자를 사용해서 깔끔하게 한 줄로 끝냈다.

<br>

공부 많이 해야겠다 정말!!

<br> 
