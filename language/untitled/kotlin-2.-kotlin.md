---
description: 기본적인 구성요소
---

# \[Kotlin 후려치기\] 2. Kotlin 기본기

## val과 var

코틀린에서 변수를 선언하기 위한 두 가지 키워드

* var : 변경 가능한 변수 선언 키워드

```kotlin
var name1 = "kotlin"

var name2: String
name2 = "kotlin"

var name3 = "kotlin"
name3 = "more kotlin"
```

* val : 읽기 전용 변수 ; java에서 final과 같은 의미
  * 생성할 때 반드시 초기화 해줘야 한다
  * **인스턴스는 여전히 함수나 프로퍼티를 통해 인스턴스의 멤버 변수가 변경되는 것을 허용한다**

```kotlin
val name = "kotlin"
```

## 타입 추론

> 코틀린은 강타입 언어임에도 불구하고, **항상 타입을 명시적으로 선언할 필요가 없다.**    
> 컴파일러는 표현식에 포함된 정보로 해당 타입을 찾으려고 시도한다.   
> 메커니즘의 오른쪽 값을 확인하는 것이다.\(오른쪽 값을 확인하면 타입이 명확해지기 때문\) 이러한 메커니즘을 타입 추론\(type inference\) 라고 부른다. **타입 추론은 보일러 플레이트 코드는 줄이면서 현대적인 언어에서 기대하는 타입 안정성은 유지한다**
>
> 함수 시그니처로 매개변수 타입을 추론하는 클로저\(closure\)에서도 사용될 수 있다.  
> 또한 함수에 있는 표현식으로 반환 값을 추론할 수 있는 한 줄짜리 함수에도 사용할 수 있다.

```kotlin
fun plusOne(x: Int) = x + 1
```

### 명시적 타입 선언

```kotlin
val explicitType: Number = 12.3
```

## 기본 타입

**kotlin에서는 모든 것이 객체다.**

따라서 자바에서 사용되던 원시타입\(primitive type\)은 kotlin에서 사용할 수 없다.

kotlin 컴파일러는 성능을 이유로 기본 타입을 가능하면 jvm 원시 타입으로 다시 매핑하려 할 것이다. 그러나 때로는 값이 박싱\(boxing ; 원시 타입을 래퍼 타입으로 전환 하는 것\)돼야 한다

* 타입이 널 값이 가능하거나\(nullable\) \(자바에서, boolean temp = null; 은 불가능\)
* 타입을 제너릭에 사용할 경우 \(제너릭은 원시타입은 불가능\)

### 숫자

| 타입 | 길이 |
| :--- | :--- |
| Long | 64 |
| Int | 32 |
| Short | 16 |
| Byte | 8 |
| Double | 64 |
| Float | 32 |

#### 숫자 리터럴 생성

```kotlin
val int = 123
val long = 123456L
val double = 12.34
val float = 12.34F
val hexadecimal = 0xAB
val binary = 0b01010101

val int = 123
val long = int.toLong()

val float = 12.34F
val double = float.toDouble()
// toByte(), toLong(), toInt(), toShort(), toDouble(), toFloat()
```

#### 비트, 논리 연산자

코틀린은 일반적인 비트연산자와 논리 연산을 지원한다

* 왼쪽 비트 이동
* 오른쪽 비트 이동
* 부호가 없는 오른쪽 비트 이동
* 논리곱\(logical and\)
* 논리합\(logical or\)
* 배타적 논리합\(exclusive logical or\)
* 역 \(inverse\)

자바와는 달리 이런 **연산자들이** 내장 연산자가 아니라 **이름이 있는 함수다** 

```kotlin
// 비트 연산자
val leftShift = 1 shl 2 // 왼쪽 비트 이동
val rightShift = 1 shr 2 // 오른쪽 비트 이동
val unsignedRightShift = 1 ushr 2 // 부호가 없는 오른쪽 비트 이동 

// 논리 연산자 
val and = 1 and 0x00001111
val or = 1 or 0x00001111
var xor = 1 xor 0x00001111
val inv = 1.inv() 
// 역(inverse)은 이항 연산자가 아니라 단항 연산자이기 때문에, 숫자에 점 연산자를 사용해서 호출 가능
```

### 불리언\(boolean\)

부정, 논리곱, 논리합 연산자를 지원  
**논리곱과 논리합은 느슨하게 평가되기 때문에, 왼쪽에서 조건을 만족한다면 오른쪽은 평가되지 않는다**

```kotlin
val x = 1
val y = 2
val z = 2

val isTrue = x < y && x < z
val alsoTrue = x == y || y == z
```

### 문자

char는 단일 문자를 나타낸다. 문자 리터럴은 ' \(단일 따옴표\)를 사용한다.  
또한, char는 \t, \b, \n, \r, ', ", \\, \$와 같은 이스케이프를 지원한다.  


모든 유니코드 문자는 유니코드 숫자를 사용해 표현할 수 있는데,   
예를 들면, \u1234와 같은 방식으로 표현할 수 있다.

**char 타입은 자바에서처럼 숫자로 다뤄지지 않는다**

### 문자열

kotlin에서도 **문자열은 불변이다.** 문자열 리터럴은 이중 따옴표나, 삼중 따옴표를 사용해 생성한다.

* 이중 따옴표 : 이스케이프된 문자열을 생성한다
* 삼중 따옴표 : 원시 문자열을 생성한다. 이스케이프가 필요하지 않으며 모든 문자를 포함할 수 있다.

```kotlin
val string = "string with \n new line"
/*
string with
new line
*/

var rawString = """
raw string is super useful for \n strings that span many lines




"""
/*

raw string is super useful for \n strings that span many lines




*/
```

### 배열

kotlin 에서는 라이브러리 함수인 arrayOf\(\)를 사용해 배열을 생성할 수 있다

```kotlin
// arrayOf를 사용한 배열 생성
var array = arrayOf(1, 2, 3) // array : [1, 2, 3]

/// 각 요소를 생성하는데 사용되는 함수로부터 배열을 생성
val perfectSquares = Array(10, {k -> k * k})
```

**kotlin 에서 배열은 일반적인 컬렉션 클래스일 뿐이다.**

또한 배열의 인스턴스는 이터레이터 함수와 get 함수, set 함수 뿐만 아니라 size 함수도 제공한다. get 함수와 set 함수는 다른 여러 C 스타일 언어에서와 마찬가지로 괄호 문법을 지원한다.

```kotlin
val element1 = array[0]
val element2 = array[1]
array[2] = 5 
```

코틀린에서는 JVM에서 결국 원시 타입으로 표현될 박싱 타입을 피하고자 이를 대체할 수 있는 배열 클래스를 제공하며, 각 원시 타입에 특화되어 있다. 이러한 배열 클래스는 일반 자바와 마찬가지로 배열을 효율적으로 사용할 수 있게 해준다.

* ByteArray
* CharArray
* ShortArray
* IntArray
* LongArray
* BooleanArray
* FloatArray
* DoubleArray 

## 패키지

패키지는 네임스페이스 단위로 코드를 나눌 수 있게 해준다.

```kotlin
package com.packt.myproject

class Foo
fun bar(): String = "bar"
```

패키지명은 클래스, 객체, 인터페이스 또는 함수에 대한 정규화된 이름\(FQN, fully qualified name\)을 제공하기 위해 사용된다. 위 예제에서 Foo 클래스는 com.packt.myproject.Foo라는 정규화된 이름을 가지며, 최상위 함수인 bar는 com.packt.myproject.bar라는 정규화된 이름을 갖는다. 

## 임포트

클래스, 객체, 인터페이스와 함수를 선언한 패키지 외부에서 이를 사용하기 위해 임포트해야만 하며, 별칭을 지어주거나 와일드 카드를 사용할 수 있다.

```kotlin
import java.io.* // 와일드카드 임포트
import java.io.path as Path // 임포트명 변경
```

## 문자열 템플릿

문자열 템플릿은 패턴 치환이나 문자열 연속이 필요하지 않으면서도 손쉽고 효과적인 방법으로 문자열 안에 값이나 변수, 심지어 표현식도 끼워 넣는다. 값이나 변수에 접두사로 달러\($\) 기호를 추가함으로써 간단하게 추가 할 수 있다.

```kotlin
val name = "Sam"
val str = "hello $name" // hello Sam 
```

임의의 표현식 같은 경우 접두사로 달러\($\)를 추가하고 괄호{}로 식을 감싸는 방식으로 추가 가능

```kotlin
val name = "Sam"
// hello Sam. Your name has 3 characters
val str = "hello $name. Your name has ${name.length} characters"
```

## 범위

범위\(range\)는 시작하는 값과 끝나는 값 사이의 간격으로 정의된다. 비교가 가능한 타입이기만 하면 범위를 생성하는 데 사용될 수 있으며, 범위는 `..` 연산자를 사용해 생성할 수 있다.

```kotlin
val aToz = "a".."z"
val oneToNine = 1..9
```

범위를 한번 생성하고 나면 주어진 값이 범위에 포함되는지 검사하기 위해 in 연산자를 사용할 수 있게 된다. **이것이 왜 타입을 비교할 수 있어야만 하는지에 대한 이유다.** 값이 범위에 포함되기 위해서는 시작값 이상 끝나는 값 이하여야 한다.

```kotlin
val aToz = "a".."z"
val isTrue = "c" in aToZ // true
val oneToNine = 1..9
val isFalse = 11 in oneToNine // false
```

## 루프

## 예외처리

## 클래스 인스턴스화하기

## 참조 동등성과 구조 동등성

## this 표현식

## 스코프

## 가시성 제어자

### private

### protected

### internal

## 표현식으로서의 흐름 제어

## 널 문법

### 똑똑한 형변환

### 명시적 형변환

## when 표현식

### when\(값\)

#### 인자가 없는 when

## 함수 반환

## 타입 체계

## 요약

