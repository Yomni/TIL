---
description: Level 1
---

# \[프로그래머스\] 크레인 인형뽑기 게임

### 문제 URL

[https://programmers.co.kr/learn/courses/30/lessons/64061](https://programmers.co.kr/learn/courses/30/lessons/64061)

### 문제 요약

격자의 상태가 담긴 2차원 배열 board에서 moves 위치 순서대로 제일 위에 있는 인형을 뽑았을 때, 2개가 연달아 만나면 없어진다. 이때 없어진 인형의 갯수 총합 return

### input

* board : Array&lt;IntArray&gt; \(n \* n 사이즈의 2차원 배열 ; 단, n은 5이상 30이하\) ex\) \[\[0,0,0,0,0\],\[0,0,1,0,3\],\[0,2,5,0,1\],\[4,2,4,4,2\],\[3,5,1,3,1\]\]
* moves : IntArray \( 1 이하 1,000 이하의 1차원 배열\) ex\) \[1,5,3,5,1,2,1,4\]

### output

크레인을 작동시킨 후 터트려져 사라진 인형의 개수를 return  
ex\) 4

### 문제 해결 전략

1. moves의 각 요소에 접근한다
2. board의 각 하위 차원 배열을 탐색한다.
3. moves의 요소 index에 접근하고, 0이 아닌 가장 상단의 요소를 탐색한다.
4. bucket\(바구니\)에 무언가 있다면, 맨 위 인형이 내가 지금 집은 인형과 일치하는지 확인 --&gt; 일치한다면, 맨 위 요소를 제거하고 answer += 2 실행 bucket\(바구니\)에 아무것도 없다면 무조건 insert
5. 빼낸 인형을 표시해준다 —&gt; 0 으로 값을 변경

1 ~ 5를 moves의 총 size만큼 반복한다

### 소스코드\(kotlin\)

```kotlin
class Solution {
    fun solution(board: Array<IntArray>, moves: IntArray): Int {
        var answer = 0
        var bucket: MutableList<Int> = mutableListOf()

        // moves 요소만큼 for
        moves.forEach {
            for (intArr in board) {
                if (intArr[it - 1] != 0) {
                    // bucket이 비어있다면
                    if (bucket.isEmpty()) {
                        bucket.add(intArr[it - 1])
                    } else {
                        if (bucket.last() == intArr[it - 1]) {
                            bucket.removeAt(bucket.lastIndex)
                            answer += 2
                        } else {
                            bucket.add(intArr[it - 1])
                        }
                    }
                    intArr[it - 1] = 0
                    break;
                }
            }
        }

        return answer
    }
}
```



