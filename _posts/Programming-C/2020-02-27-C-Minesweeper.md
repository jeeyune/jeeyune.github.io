---
layout: post
title: "[C언어] C언어 코딩도장 Unit 38 지뢰찾기 문제"
comments: true
categories: [Programming/C]
tags: [C, Memory, Data Structures]
---

이번 포스팅은 'C언어 코딩도장'의 <Unit 38 포인터와 배열 응용하기>에 나와있는 지뢰찾기 문제의 답입니다.    
<br>

### 문제
<br>
표준 입력으로 행렬의 크기 m, n과 문자(char) 행렬이 입력됩니다(m과 n의 범위는 3~10). 입력된 m, n은 공백으로 구분되며 행렬 안에서 *은 지뢰이고 .은 지뢰가 아닙니다. 지뢰가 아닌 요소에는 인접한 지뢰의 개수를 출력하는 프로그램을 만드세요(scanf 함수 호출 전에 문자열을 출력하면 안 됩니다).

여러 줄을 입력 받으려면 다음과 같이 for 반복문으로 scanf를 반복 호출하면 됩니다.

```c
for (int i = 0; i < m; i++)
{
    scanf("%s", matrix[i]);
}
```

행렬의 가로 공간에는 문자열이 들어갑니다. 따라서 메모리를 할당할 때는 n + 1(가로 크기 + 1)만큼 할당하여 NULL이 들어갈 공간까지 확보해야 합니다.

<br>
예)
<br>

입력
<br>
5 5   <br>
&#42; . . . . <br>
.	&#42; .	&#42;	&#42; <br>
. &#42; . . . <br>
. . . . . <br>
. . . . . <br>

<br>

출력
<br>

&#42; 2 2 2 2  <br>
3 &#42; 3 	&#42; 	&#42;  <br>
2 &#42; 3 2 2  <br>
1 1 1 0 0  <br>
0 0 0 0 0  <br>

<br><br>


## 코드
<br>
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdlib.h>
#include <stdio.h>
#include <string.h>

int main(){
    int m, n;                
    int mine_counter = 0;                                                       // 주변 지뢰 카운터
    int i, j;

    scanf("%d %d", &m, &n);                                                     // 행렬의 크기 입력

    char **minesweeper = malloc(sizeof(char *) * m);                            // 행렬의 세로(가로줄) 할당

    for(i = 0; i < m; i++){                                                     // 세로 크기만큼 반복
        minesweeper[i] = malloc(sizeof(char) * (n + 1));                        // 가로 크기만큼 반복
        memset(minesweeper[i], 0, sizeof(char) * (n + 1));                      // 각 요소를 0으로 초기화
    }

    for(i = 0; i < m; i++){                                                     // 문자열 입력
        scanf("%s", minesweeper[i]);
    }

    for(i = 0; i < m; i++){                                                     // 배열의 요소를 검색 후 '*' 와 같으면 넘어감
        for(j = 0; j < n; j++){
            if(minesweeper[i][j] == '*'){
                printf("%c", minesweeper[i][j]);
                continue;
            }

            else{                                                               // '*'와 같지 않으면 현재 위치 주변 8개
                for(int y = i - 1; y <= i + 1; y++){                            // (왼쪽 위 대각선, 위, 오른쪽 위 대각선,
                    for(int x = j - 1; x <= j + 1; x++){                        //  왼쪽, 오른쪽
                        if(y < 0 || x < 0 || y >= m || x >= n) continue;        //  왼쪽 아래 대각선, 아래, 오른쪽 아래 대각선)
                        else if(minesweeper[y][x] == '*') mine_counter += 1;    // 범위를 벗어나면 넘어가고, 검색했을때 '*'와 같다면 mine_counter에 1씩 추가
                    }
                }
                minesweeper[i][j] = mine_counter;                               // 해당 위치에 지뢰 갯수 표시 후 mine_counter는 0으로 초기화
                printf("%d", minesweeper[i][j]);
                mine_counter = 0;
            }
        }
        printf("\n");
    }

    for(int i = 0; i < m; i++){                                                 // 할당한 메모리 해제
        free(minesweeper[i]);
    }

    free(minesweeper);

    return 0;
}

```
<br>

아직 많이 부족한 부분이라 많이 부끄럽지만 혹시나 도움이 필요하신 분이 계실까 공유합니다!
<br>
조언이나 틀린부분 지적 환영합니다 :)
