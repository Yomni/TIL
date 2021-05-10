---
description: Level 1
---

# \[프로그래머스\] 소수 만들기

### 문제 URL

[https://programmers.co.kr/learn/courses/30/lessons/12977](https://programmers.co.kr/learn/courses/30/lessons/12977)

### 문제 요약

주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return

### input

* 서로 다른 숫자들이 들어있는 배열 nums nums의 길이는 3이상, 50 이하 nums의 각 원소는 1 이상 1000이하의 자연수, 중복 X

ex\) nums : \[1, 2, 3, 4\]

### output

nums의 서로 다른 원소 3개를 뽑아서 더했을 때 소수가 만들어지는 갯수  
ex\) 1 + 2 + 4 = 7 // 1개

### 문제 해결 전략

1. nums의 서로다른 원소 각각 3개에 접근\(3중 for문 혹은 combination 구현\)
2. 각 원소를 더한 값이 소수 인지 확인\(별도 function\)
3. 소수라면, counting

### 소스코드\(kotlin\)

```kotlin
class Solution {
    fun solution(nums: IntArray): Int {
        var answer = 0
        nums.sort()
        for(index1 in nums.indices) {
            for(index2 in nums.indices) {
                if(index1 >= index2)
                    continue
                for(index3 in nums.indices) {
                    if(index2 >= index3)
                        continue
                    if(isPrime(nums[index1] + nums[index2] + nums[index3])) {
                        answer++
                    }
                }
            }
        }
        return answer
    }


    fun isPrime(candidate: Int) : Boolean {
        var flag = true
        for(i in 2..(candidate / 2)) {
            if(candidate % i == 0) {
                flag = false
                break
            }
        }
        return flag
    }
}
```



