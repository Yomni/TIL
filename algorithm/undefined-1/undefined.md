---
description: Level 1
---

# \[프로그래머스\] 키패드 누르기

### 문제 URL

[https://programmers.co.kr/learn/courses/30/lessons/67256?language=kotlin](https://programmers.co.kr/learn/courses/30/lessons/67256?language=kotlin)

### 문제 요약

이 전화 키패드에서 왼손과 오른손의 엄지손가락만을 이용해서 숫자만을 입력하려고 합니다.  
맨 처음 왼손 엄지손가락은 `*` 키패드에 오른손 엄지손가락은 `#` 키패드 위치에서 시작하며, 엄지손가락을 사용하는 규칙은 다음과 같습니다.

1. 엄지손가락은 상하좌우 4가지 방향으로만 이동할 수 있으며 키패드 이동 한 칸은 거리로 1에 해당합니다.
2. 왼쪽 열의 3개의 숫자 `1`, `4`, `7`을 입력할 때는 왼손 엄지손가락을 사용합니다.
3. 오른쪽 열의 3개의 숫자 `3`, `6`, `9`를 입력할 때는 오른손 엄지손가락을 사용합니다.
4. 가운데 열의 4개의 숫자 `2`, `5`, `8`, `0`을 입력할 때는 두 엄지손가락의 현재 키패드의 위치에서 더 가까운 엄지손가락을 사용합니다. 4-1. 만약 두 엄지손가락의 거리가 같다면, 오른손잡이는 오른손 엄지손가락, 왼손잡이는 왼손 엄지손가락을 사용합니다.

눌러야 하는 번호의 숫자 배열과, 왼손잡이 / 오른손잡이 에 대한 정보를 주어질 경우 어떤 손으로 숫자 배열을 누르게 되는지 Return

### input

* numbers 배열 numbers의 크기는`1` 이상 `1,000` 이하 numbers 배열 원소의 값은 `0` 이상 `9` 이하인 정수
* hand
  * `"left"` 혹은 `"right"` 
  * `"left"` : 왼손잡이
  * `"right"` : 오른손잡이



| numbers | hand |
| :--- | :--- |
| \[1, 3, 4, 5, 8, 2, 1, 4, 5, 9, 5\] | `"right"` |

### output

* 왼손 엄지손가락을 사용한 경우는 `L`, 오른손 엄지손가락을 사용한 경우는 `R`을 순서대로 이어붙여 문자열 형태로 return

result : `"LRLLLRLLRRL"` 

### 문제 해결 전략

1. 
### 소스코드\(kotlin\)

```kotlin
class Solution {
    fun solution(numbers: IntArray, hand: String): String {
        var answer = ""
        return answer
    }
}
```

