# \[프로그래머스\] 두 개 뽑아서 더하기

### 문제 URL

[https://programmers.co.kr/learn/courses/30/lessons/68644?language=kotlin](https://programmers.co.kr/learn/courses/30/lessons/68644?language=kotlin)

### 문제 요약

주어진 정수배열 numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 

### input

numbers : intArray \(단, 길이는 2 이상 100 이하\)

ex\) \[2, 1, 3, 4, 1\]

### output

numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수의 배열\(단, 오름차순\)

ex\) \[2, 3, 4, 5, 6, 7\]

### 문제 해결 전략

Set\(중복 허용 X\) 자료구조를 활용한 문제 해결,   
특히 sortedSet\(입력 시 데이터를 자동으로 정렬\)을 활용

### 소스코드\(kotlin\)

```kotlin
class Solution {
    fun solution(numbers: IntArray): IntArray {
        val answer: MutableSet<Int> = sortedSetOf()
        numbers.forEachIndexed { index, i -> 
            numbers.forEachIndexed { idx, it ->  
                if (index != idx) 
                    answer.add(i.plus(it))
            }
        }
        return answer.toIntArray()
    }
}
```



