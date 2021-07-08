---
description: 함수형 프로그래밍으로의 첫발
---

# \[Kotlin 후려치기\] 4. Kotlin과 함수

## 함수 정의하기

* fun 키워드를 이용하여 정의
* 매개변수 목록은 매개변수를 정의하지 않는다 하더라도 반드시 존재 '\(\)'
* 각 매개변수는 '이름 : 타입' 형식
* 모든 함수는 반환값이 있어야 한다.
  * 단, 반환값이 없는 경우 Unit을 반환하도록 정의 \(Unit은 생략 가능\) ; java의 void

```kotlin
// 매개변수가 없는 함수
// return 키워드를 생략해도 가능하다
fun hello(): String = "hello world" 

// 매개변수 존재
fun hello(name:String, location:String):String = "hello to you $name at $location"

// Unit을 반환하도록 정의
fun print1(str:String): Unit {
    println(str)
}

// Unit 생략
fun print2(str:String) {
    println(str)
}
```

## 단일 표현식 함수, 한 줄짜리 함수\(single line ; one line\)

* 함수의 정의가 **단일 표현식으로 되어 있는 경우 반환 타입을 생략 가능**
* 컴파일러가 자유롭게 추론

```kotlin
fun square(k: Int) = k * k
```

## 멤버 함수

* 클래스나 객체 또는 인터페이스 내부에 선언
* 멤버 함수는 자신끼리 참조 가능하며 이 때, 인스턴스 이름은 필요 없다.

```kotlin
val string = "hello" // string 인스턴스
val length = string.take(5) // string 인스턴스에 존재하는 take라는 함수 호출

object Rectangle {
    fun printArea(width: Int, height: Int) : Unit {
        // 멤버함수 호출, 인스턴스나 클래스 또는 객체 명이 필요 없다
        val area = calculateArea(width, height)
        println("The area is $area")
    }
    
    fun calculateArea(width: Int, height: Int): Int {
        return width * height
    }
}
```

## 지역 함수

코틀린에서 **다른 함수 내부에 함수를 선언**하도록 지원한다. 이를 통해 **반복적인 작업을 더욱 효율적으로 쪼갤** 수 있다. 이런 함수를 **지역\(local\) 함수 또는 중첩\(nested\) 함수**라 부른다. 함수는 여러 번 중첩될 수도 있다.

```kotlin
fun printArea(width: Int, height: Int): Unit {
    fun calculateArea(): Int = width * height
    val area = calculateArea(width,height)
    println("The area is $area")
}

// fizz buzz : 시작 값부터 마지막 값까지 정수를 출력하는 것, 
// fizz : 3의 배수인 정수인 경우
// buzz : 5의 배수인 정수인 경우
// fizz & buzz : 3과 5의 공배수인 경우
fun fizzbizz(start: Int, end: Int): Unit {
    for (k in start..end) {
        
        fun isFizz(): Boolean = k % 3 == 0
        fun isBuzz(): Boolean = k % 5 == 0
        
        when {
            isFizz() && isBuzz() -> println("Fizz Buzz")
            isFizz() -> println("Fizz")
            isBuzz() -> println("Buzz")
            else -> println(k)
        }
    }
}
```

장점

1. 스코프 바깥에 선언한 매개변수나 변수에 접근 가능
2. for 루프나 while루프, 그 밖의 블록 내부에도 정의할 수 있다.

## 최상위 함수\(top - level\)

최상위 함수\(top - level\)는 클래스, 객체 또는 인터페이스 바깥에 존재하는 함수이며 파일 내부에서 바로 정의하는 함수이다. 주로 도우미 함수나 유틸리티 함수를 정의하는 데 유용하다. 

자바에서는 객체가 아무런 값을 가지지 않는 경우에는 도우미 클래스 내에 정적 함수 형태로 존재한다.\(예를 들어, 자바 표준 라이브러리에 있는 컬렉션 함수 같은 경우...\)

몇몇 함수는 독립적으로 사용하는 경우가 있다.  
ex\) require, check, error, requireNotNull, Assertions ...

```kotlin
// require : 함수가 호출 됐을 때 매개변수가 불변 조건을 만족함을 보장하는 데 사용
fun foo(k : Int) {
    // 매개 변수가 항상 10보다 커야하는 경우를 보장
    require(k > 10, {"k should be greater than 10"} )
}
```

## 이름이 있는 매개변수

이름이 있는 매개변수\(named parameter\)는 함수에 인자를 전달할 때 인자에 이름을 명시할 수 있게 해준다. 매개변수가 여러 개인 함수의 경우, 명시적으로 이름을 붙이면 각 인자의 의도가 명확해진다는 장점이 있다. 이는 호출하는 쪽에서 코드를 좀 더 읽기 쉽게 해준다.

```kotlin
// 첫 번째 문자열이 두 번째 문자열의 일부를 포함하는지를 확인
val string = "a kindness of ravens"
string.regionMatches(thisOffset = 14, other = "Red Ravens", 
    otherOffset = 4, length = 6, ignoreCase = true)
    
// 호출자에 맞춰 매개변수 순서를 변경하는 것도 허용
val string = "a kindness of ravens"
string.endsWith(suffix = "ravens", ignoreCase = true)
string.endsWith(ignoreCase = true, suffix = "ravens")
```

이름이 있는 매개변수가 왜 유용한지는 '기본 값을 갖는 매개변수'의 경우에서 확인할 수 있다. 매개변수의 순서를 변경하는 것은 어떤 기본값을 오버라이딩할지를 선택할 수 있게 해준다.

## 기본 값을 갖는 매개변수

자바에서는 **똑같은 동작을 하는 메서드를 오버로딩을 통해 사용자의 입맛에 맞게 매개변수의 갯수나 형태를 바꾸어 가며 사용**할 수 있다. 하지만, 다수의 매개변수는 같은 함수를 오버로딩한 다양한 변형을 갖게 되고 끝없는 보일러플레이트를 발생시킨다.  
ex\) Java의 BigDecimal divide 메소드

```java
public BigDecimal divide(BigDecimal divisor)
public BigDecimal divide(BigDecimal divisor, RoundingMode roundingMode)
public BigDecimal divide(BigDecimal divisor, int scale, RoundingMode roundingMode)
```

이런 단점을 극복하고자 **코틀린에서는 기본 값을 갖는 매개변수를 제공**한다. **하나 이상의 매개변수가 기본 값을 갖도록 정의**할 수 있으며, 각 값은 인자가 지정되지 않을 경우 사용된다. 이로써 **매개변수의 종류나 형태가 다양할 경우에도 단일 함수로 정의**할 수 있도록 도와준다. 

```kotlin
fun divide(divisor: BigDecimal, scale: Int = 0, 
    roundingMode: RoundingMode = RoundingMode.UNNECESSARY): BigDecimal
    
// 사용 예시
divide(BigDecimal(12.34))
divide(BigDecimal(12.34), 8)
divide(BigDecimal(12.34), 8, RoundingMode.HALF_DOWN)

// 다음과 같이는 사용할 수 없다
divide(BigDecimal(12.34), RoundingMode.HALF_DOWN) // 오류

// 이 때 이름이 있는 매개변수 기능으로 극복 가능
divide(BigDecimal(12.34), roundingMode = RoundingMode.HALF_DOWN) // 정상작동
```

기본 값이 있는 매개변수는 생성자에서도 사용이 가능하다. 이를 통해 생성자 오버로딩은 필요 없게 된다. 

## 확장 함수

확장 함수란 **특정 타입의 인스턴스에서 사용가능한 함수를 추가 정의\(확장\)하는 것**을 말한다.  
예를 들어, list 컬렉션에서 reverse나 drop 같은 함수를 정의해야할 때, 자바에서는 서브 클래스를 재정의 하거나, 별도의 메소드를 구현하여 사용해야 한다.

```java
// 별도 메소드를 구현한 경우 사용
reverse(take(3, drop(2, list)))
```

이러한 경우 가독성이 매우 떨어지며, IDE에서 제공하는 코드 완성\(code completion\)을 사용할 수 없다.

만약, list 인스턴스에서 이러한 함수에 직접 접근할 수 있다면?

```kotlin
// 가독성 좋고 매우 유연하게 동작한다
list.drop(2).take(3).reverse()
```

코틀린에선 이런 함수를 **확장 함수\(extension function\)라고 정의**한다. 또한 **확장 함수가 사용될 인스턴스 타입은 수신자 타입\(receiver type\)** 이라 불린다.  예시로 drop 함수를 list의 확장 함수로 구현한 코드이다.

```kotlin
fun <E> List<E>.drop(k: Int): List<E> {
    val resultSize = size - k
    when {
        resultSize <= 0 -> return emptyList<E>()
        else -> {
            val list = ArrayList<E>(resultSize)
            for (index in k..size - 1) {
                list.add(this[index]) // this를 사용하고 있음에 주의
            }
            return list
        }
    }
}
```

**함수 몸체에서 this 키워드**를 사용하고 있는데, 이는 **수신자 인스턴스를 참조하기 위해 사용**되며, **수신자 인스턴스란 함수가 호출되는 객체**를 말한다. 확장 함수 내부에 있을 때마다 this 키워드는 항상 수신자 인스턴스를 참조하며, 바깥 범위에 있는 인스턴스는 제한돼야 한다. 

### 확장 함수의 우선순위

확장 함수는 클래스나 인스턴스에 정의된 함수를 오버라이딩할 수 없다. 완전히 같은 시크니처로 확장 함수를 정의할 경우\(이름, 매개변수, 타입, 순서와 반환 타입까지 모두 같은 경우\) 컴파일러는 이를 절대로 호출하지 못할 것이다.

따라서 확장 함수의 우선순의는 클래스나 인스턴스에 정의된 함수를 더 높게 잡고 있으며, 시그니처가 동일한 확장 함수는 절대로 호출될 수 없다. 만약 확장 함수를 정의하려면 기존 클래스나 인스턴스에 정의되지 않은 시그니처로 정의해야 한다.

```kotlin
class Submarine{
    fun fire(): Unit {
        println("Firing torpedoes")
    }
    
    fun submerge(): Unit {
        println("Submerging")
    }
}

// 시그니처가 기존 클래스와 동일하기 때문에 
// 이 확장 함수는 절대로 호출될 일 없다.
fun Submarine.fire(): Unit {
    println("Fire on board!")
}

fun Submarine.submerge(depth: Int): Unit {
    println("Submerging to a depth of $depth fathoms")
}

val sub = Submarine()
sub.fire() // Firing torpedoes
sub.submerge() // Submerging
sub.submerge(10) // Submerging to a depth of 10 fathoms
```

### 널 값에서의 확장 함수

널 값에서도 확장 함수를 지원한다. 이러한 상황에서는 참조가 널 값을 갖게 되므로 널 참조를 안전하게 처리하지 못하는 Any 함수는 널 포인터 익셉션을 발생시킬 것이다. 아래 기능은 널 값을 갖더라도 안전하게 사용할 수 있도록 equals 함수를 오버로딩하는 방법을 보여준다.

```kotlin
fun Any?safeEquals(other: Any?): Boolean {
    if (this == null && other == null) return ture
    if (this == null) return false
    return this.equals(other)
}
```

### 멤버 확장 함수

확장 함수는 일반적으로 최상위 단계에 선언하지만, 클래스 내부에 멤버로 선언하여 확장 함수의 범위를 제한할 수도 있다.

```kotlin
class Mappings {
    private val map = hashMapOf<Int, String> ()
    private fun String.stringAdd(): Unit {
        // hashCode()는 Mappings의 인스턴스도 가지고 있는 함수(dispatch receiver)
        // 문자열 인스턴스에서도 가지고 있는 함수(extension receiver)
        map.put(this@Mappings.hashCode(), this)
    }
    
    fun add(str: String): Unit = str.stringAdd()
}
```

* hashCode 함수는 Any에 정의되어 있으므로, Mappings의 인스턴스도 String의 인스턴스도 모두 가지고 있는 함수이다. 이 때, Mappings의 hashCode 함수는 **디스패치 수신자\(dispatch receiver\)** 라고 하며, String 인스턴스의 HashCode 함수는 **확장 수신자\(extension receiver\)**라고 한다.

### 멤버 확장 함수 오버라이딩 하기

### 컴패니언 오브젝트 확장

### 다중 값 반환

### 중위 함수

## 연산자

### 연산자 오버로딩

### 기본 연산자

### in/contains

### get/set

#### invoke

### 비교

### 할당

### 자바 상호 운용

## 함수 리터럴

## 꼬리 재귀 함수

## 가변 인자

### 전개 연산자

## 표준 라이브러리 함수

### apply

### let

### with

### run

### lazy

### use

### repeat

### require

### assert

### check

## 제너릭 함수

## 순수 함수

## 코틀린에서 자바 사용하기

### 게터와 세터

### 단일 추상 메소드

### 코틀린 식별자 탈출하기

### 자바 void 메소드

## 자바에서 코틀린 사용하기

### 최상위 함수

### 기본 매개변수

### 오브젝트와 정적 메소드

### 이름 삭제하기

### 확인된 예외



