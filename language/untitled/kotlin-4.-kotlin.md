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

## 최상위 함수

## 이름이 있는 매개변수

## 기본 값을 갖는 매개변수

## 확장 함수

### 확장 함수의 우선순위

### 널 값에서의 확장 함수

### 멤버 확장 함수

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



