---
description: Kotlin 공식 Docs 에서 말하는 Kotlin의 장점
---

# \[Kotlin 후려치기\] 1. Kotlin을 사용해야 하는 이유

### 1. Concise \( 간결함 \)

* 한 줄로 getters, setters, equals\(\), hashCode\(\), toString, copy\(\)가 있는 POJO를 만들 수 있습니다.

```kotlin
/*
 Create a POJO with getters, setters, `equals()`, `hashCode()`, `toString()` and `copy()` in a single line:
*/

data class Customer(val name: String, val email: String, val company: String)

// Or filter a list using a lambda expression:

val positiveNumbers = list.filter { it > 0 }

// Want a singleton? Create an object:

object ThisIsASingleton {
    val companyName: String = "JetBrains"
}
```

### 2. Safe \( 안정성 \)

* 가장 대표적인 실수인 NullPointerExceptions를 없앨 수 있습니다.

```kotlin
/*
 Get rid of those pesky NullPointerExceptions, you know, The Billion Dollar Mistake
*/

var output: String
output = null   // Compilation error

// Kotlin protects you from mistakenly operating on nullable types

val name: String? = null    // Nullable type
println(name.length())      // Compilation error

// And if you check a type is right, the compiler will auto-cast it for you

fun calculateTotal(obj: Any) {
    if (obj is Invoice)
        obj.calculateTotal()
}
```

### 3. Interoperable \( 상호 운용성 \)

* SAM 지원을 포함하여, 100% 호환성이 있으므로 JVM의 기존 라이브러리를 사용하십시오.

```kotlin
/*
 Use any existing library on the JVM, as there’s 100% compatibility, including SAM support.
*/

import io.reactivex.Flowable
import io.reactivex.schedulers.Schedulers

Flowable
    .fromCallable {
        Thread.sleep(1000) //  imitate expensive computation
        "Done"
    }
    .subscribeOn(Schedulers.io())
    .observeOn(Schedulers.single())
    .subscribe(::println, Throwable::printStackTrace)
```

* JVM 또는 JavaScript를 대상으로 합니다. Kotlin에 코드를 작성하고 배포할 위치를 결정하십시오.

```kotlin
// Target either the JVM or JavaScript. Write code in Kotlin and decide where you want to deploy to

import kotlin.browser.window

fun onLoad() {
    window.document.body!!.innerHTML += "<br/>Hello, Kotlin!"
}
```

> https://Kotlinlang.org를 참고하여 작성하였습니다.

