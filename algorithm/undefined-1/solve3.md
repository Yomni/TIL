---
description: Level 1
---

# \[프로그래머스\] 내적

### 문제 URL

[https://programmers.co.kr/learn/courses/30/lessons/70128](https://programmers.co.kr/learn/courses/30/lessons/70128)

### 문제 요약

길이가 같은 두 1차원 정수 배열 a, b가 매개변수로 주어집니다. a와 b의 [내적](https://en.wikipedia.org/wiki/Dot_product)을 return 

### input

* 두 정수 배열 a, b
* a, b 는 길이가 같다

ex\) a : \[1, 2, 3, 4\]         b : \[-3, -2, 0, 2\]

### output

a와 b의 내적의 결과를 return  
ex\) \(1 \* -3\) + \(2 \* -2\) + \(3 \* 0\) + \(4 \* 2\) = 3

### 문제 해결 전략

1. a와 b의 길이가 같으므로, 둘 중 아무거나 길이만큼 반복
2. 0으로 초기화 된 정수형 변수에 a\[index\] \* b\[index\] 를 더한다.
3. 길이만큼 반복

### 소스코드\(kotlin\)

```kotlin
class Solution {
    fun solution(a: IntArray, b: IntArray): Int {
        var answer: Int = 0
        a.forEachIndexed { index, i ->
            answer += i * b[index]
        }
        return answer
    }
}
```



