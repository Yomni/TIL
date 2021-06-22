---
description: 알고리즘 분석 ; 정확성 증명
---

# \(writing\)5. Algorithm Analysis ; Correctness Proof

> 이 Sector는 주로 알고리즘의 정확성 증명에 대한   
> 이론적인 내용을 다루므로 흥미가 없으신 분들은 건너 뛰셔도 무방합니다.

### Q&gt; 어떤 알고리즘이 정확히 구동 된다고 확신할 수 있는가?

A&gt; 정확성 증명에 의해 정확히 구동 된다고 대답할 수 있다.

## Literative Algorithm\(반복문\) vs Recursive Algorithm\(재귀\)

### Literative Algorithm를 통한 정확성 증명

Loop invariant를 주로 사용 ==&gt; 프로그래밍의 흐름제어로는 반복문으로 주로 해결

1. 주어진 Algorithm의 Specification을 명시
   * Specification : 어떤 Input에 대해 어떤 Output이 나오는 것을 예상한 값 혹은 로직
2. 각 Loop에 대해..\(for, while 등등..\)
   1. Loop Invariant를 찾는다
      * Loop Invariant : Loop에서 1번 반복할 때마다 변화되는 내용
      * 변화되는 내용이 어떻게 활용될 것인가?
   2. Loop invariant를 증명한다

Ex\) Multiply \( y, z\) // y \* z를 return 한다. 이 때, Specification은 y \* z

```kotlin
fun Multiply(y:Int, z:Int):Int {
    var x = 0
    var ytmp = y
    var ztmp = z
    
    // 2진수로 변환 후 곱셈
    while(ztmp > 0){
        x = x + (ytmp * (ztmp % 2))
        ytmp = 2 * ytmp
        ztmp = ztmp / 2
    }
    return x
}
```

1. Specification : 임의의 자연수 y, z에 대하여, multiply\(y, z\)를 호출하면 y \* z가 return 된다.

