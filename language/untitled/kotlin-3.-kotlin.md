---
description: '고차 함수, 람다식, 객체 지향 프로그래밍 언어 로서의 코틀린의 특성'
---

# \[Kotlin 후려치기\] 3. Kotlin 코틀린과 객체 지향 프로그래밍

## 객체 지향적인 언어로서의 코틀린

### 객체 지향적인 추상화의 특징

* **모든 것은 객체다** : 객체는 그저 설계나 정의에 의해 설정되고 할당된 메모리 블록, 주어진 문제 속에서 논리적인 엔티티를 가지고 이를 프로그램 안에서 객체로 전환한다.
* **객체는 메시지를 보내고 받는 방식으로 통신한다\(객체 관점\)** : 프로그램은 각 객체가 노출한 메소드를 호출한 결과로 각기 다른 동작을 수행하는 객체들의 집합이 된다.
* **객체는 자신만의 메모리를 갖는다\(객체 관점\)** : 다른 객체를 합성함으로써 객체를 생성할 수 있다.
* **모든 객체는 클래스의 인스턴스다\(반드시 객체여야 한다\)**  : 클래스는 타입이 할 수 있는 것을 명시한 청사진으로 생각할 수 있다.
* **클래스는 인스턴스를 위한 공유되는 행위를 갖는다\(프로그램 리스트에서 객체의 형태로\)** : 특정 타입의 객체는 모두 같은 메시지를 받을 수 있다. ; 객체는 같은 메소드를 노출한다.

코틀린은 위 내용을 모두 지원하면서도 OOP 언어의 세 가지 기둥인

* **캡슐화\(encapsulation\)** : 연관된 필드와 메소드 그룹을 객체로 다룬다
  * 캡슐화를 통해 각 클래스는 **신중하고 독립적으로 유지**
  * 이를 사용하는 다른 코드가 계약 조건을 유지하는 동안에는 해당 코드에 영향을 주지 않으면서 자신의 구현을 변경할 수 있다.
* **상속\(inheritance\)** : 이미 존재하는 클래스로부터 새로운 클래스를 생성할 수 있다
* **다형성\(polymorphism\)** : 각 클래스마다 자신의 메소드를 다르게 구현했음에도 각기 다른 클래스를 상호 교환하면서 사용할 수 있다

를 지원한다.

OOP 추상화는 대규모 코드에서 발생할 수 있는 문제를 완화하는데 큰 도움이 된다. OOP 추상화는 다음과 같은 기능들을 제공함으로써 코드를 유연하고 유지하기 쉽게 개선해줄 수 있다.

* **단순성** : 프로그램 객체는 현실을 모델링하므로, 복잡성은 줄이고 프로그램 구조는 단순화 한다.
* **모듈성** : 각 객체의 내부 동작은 시스템의 다른 부분과 분리되어 있다.
* **가변성** : 설계를 올바르게 했다면 객체 내부를 변경해도 프로그램의 다른 부분에 영향을 주지 않는다.
* **확장성** : 객체의 요구사항은 빈번하게 바뀌며, 새로운 객체를 추가하거나 이미 존재하는 객체를 변경하는 방법으로 이러한 요구사항에 빠르게 대응할 수 있다.
* **재활용성** : 객체는 다른 프로그램에서 사용될 수 있다.

### tip\) **OOP의 5원칙\(SOLID\)**

* **S \(SRP : Single Responsibility Principle\)** _한 클래스는 하나의 책임만 가져야 한다_
* **O \(OCP : Open / Closed Principle\)** _확장에는 열려\(Open\) 있으나, 변경에는 닫혀\(Closed\) 있어야 한다._
* **L \(LSP : Liskov's Substitution Principle\)** _프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다._
* **I \(ISP : Interface Segregation Principle\)** _특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다_
* **D \(DIP : Dependency Inversion Principle\)** _추상화에 의존한다. 구체화에 의존하면 안된다_

## 클래스

_클래스는 객체의 청사진으로, 타입의 데이터와 행위를 나타낸다_

```kotlin
class Deposit {
    // 필드
    // 프로퍼티
    // 메소드
}
```

* 자바와는 달리 하나의 소스파일 내에서 여러 개의 클래스를 정의할 수 있다.
* 접근레벨은 class 키워드 앞에 명시할 수 있으며, default 값은 public 이다.
* 생성자는 명시하지 않을 경우 컴파일러에서 자동으로 만들어 준 빈 생성자를 갖고 있다.
* new 키워드는 사용하지 않는다
* 주 생성자의 인자는 '**프로퍼티**'이다\(**필드가 아님**\)
* 생성자에 직접 접근하는 것을 원치 않는 경우
  * private : 일반적인 싱글톤 디자인에서 많이 쓰임 \(getInstance\(\) 메소드를 구현하여 유일한 인스턴스 반환\)
  * protected : 추상 클래스를 정의하는 경우 --&gt; 파생된 클래스에서만 생성자를 호출
  * internal : 모듈 로직에서 사용

```kotlin
// 별도의 주 생성자를 선언하는 법
class Person constructor(val firstName: String, val lastName: String, val age: Int?) {
}

// 주 생성자가 코드를 가지는 방법 --> init 블록으로 지정
class Person constructor(val firstName: String, val lastName: String, val age: Int?) {
    // 표현식이 false일 경우 --> IllegalArgumentException을 발생시킨다
    init {
        require(firstName.trim().length > 0) {"Invalid firsntName argument."}
        require(lastName.trim().length > 0) {"Invalid lastName argument."}
        if (age != null) {
            require(age >= 0 && age < 150) { "Invalid age argument." }
        }
    }
    
    // 두번째 생성자 선언
    // this를 통해 주 생성자 호출
    constructor(firstName: String, lastName: String) : this(firstName, lastName, null)
}

// 생성자 인자에 접두사로 val 이나 var를 반드시 붙일 필요는 없다. 만약 게터(getter)나
// var를 사용하는 경우에는 세터(setter) 메소드가 필요 없는 경우에는 항상 다음과 같이 할 수도 있다.
// 아래의 경우 getName() 과 getAge() 메소드만 게터(getter)로 사용
class Person2(firstName: String, lastName: String, howOld: Int?) {
    private val name: String
    private val age: Int?
    
    init {
        this.name = "$firstName,$lastName"
        this.age = howOld
    }
    
    fun getName(): String = this.name
    
    fun getAge(): Int? = this.age
}

```

> 클래스와 객체
>
> * 클래스 : 객체의 정의를 그린 일종의 청사진
> * 객체 : 클래스 정의에 대한 런타임 인스턴스

### 중첩 클래스

중첩 클래스 : 다른 클래스 몸체 내부에 클래스를 생성하는 개념

```kotlin
class OuterClassName {
    class NestedClassName {
    }
}
```

* 중첩클래스에도 접근레벨 설정 가능
  * private : 내부 중첩 클래스의 객체는 OuterClassName 스코프 내부에서만 생성 가능
  * internal : 모듈 내부에서만 생성 가능
  * protected : OuterClassName으로 파생된 클래스는 중첩 클래스 객체 생성 가능
* 정적 클래스 / 비정적 클래스 형태의 중첩 클래스 생성 가능
  * static class % : 정적 중첩 클래스\(static nested class\)
    * 외부 클래스의 static 멤버로만 접근 가능
  * class % : 내부 클래스\(inner class\) 
    * 외부 클래스 멤버가 private로 선언되어 있어도 내부 클래스에서 접근 가능
    * 내부 클래스의 인스턴스를 생성하기 위해서 Outer 클래스의 인스턴스가 필요하다
* 중첩 클래스는 해당 클래스를 둘러싼 클래스의 멤버로 간주

```kotlin
// 정적 중첩 클래스와 유사한 클래스를 코틀린에서 생성
class BasicGraph(val name: String) {
    class Line(val x1: Int, val y1: Int, val x2: Int, val y2: Int) {
        fun draw(): Unit {
            println("Drawing Line from ($x1:$y1) to ($x2:$y2)")
        }
    }
    
    fun draw() {
        println("Drawing the graph $name")
    }
}

val line = BasicGraph.Line(1,0,-2,0)
line.draw() // Drawing Line from (1:0) to (-2:0)
```

private의 멤버를 내부에서 접근하기 위해선, 내부 클래스 앞에 inner 키워드를 추가해 Line 클래스를 내부 클래스\(inner\)로 만들면 된다.

```kotlin
class BasicGraph(graphName: String) {
    private val name: String
    
    init {
        name = graphName
    }
    
    inner class InnerLine(val x1: Int, val y1: Int, val x2: Int, val y2: Int) {
        fun draw(): Unit {
            println("Drawing Line from ($x1:$y1) to ($x2:$y2) for graph $name")
        }
    }
    
    fun draw() {
        println("Drawing the graph $name")
    }
}

val graph = BasicGraph("sample graph")
val line = graph.InnerLine(1,0,-2,0)
line.draw() // Drawing Line from (1:0) to (-2:0) for graph sample graph
```

this 보다 더 강력한 this@label을 이용하여 명확하게 참조

```kotlin
fun main() {
	val a = A()
    a.B().foo("test")
}


class A {
    private val somefield: Int = 1
    inner class B {
        private val somefield: Int = 2
        fun foo (s: String) {
            println("Field <somefield> from B" + this.somefield) // 2
            println("Field <somefield> from B" + this@B.somefield) // 2
            println("Field <somefield> from A" + this@A.somefield) // 1
        }
    }
}
```

UI 코드 작업 시 UI 컴포넌트\(리스트 박스 or 버튼 등등..\)에서 발생하는 각기 다른 이벤트를 제어하기 위해 이벤트 핸들러를 제공해야 하는 상황이 있다.

UI 프레임워크에서는 사용자가 클래스의 인스턴스를 제공하기를 기대한다. 사용자는 이러한 리스터 클래스에서 바깥 클래스 스코프에 있는 몇몇 상태에 접근하고 싶을 것이다. 결국 사용자는 다음 예제에서와 같이 버튼의 클릭수를 세기 위해 익명의 내부 클래스를 제공하게 될 것이다.

```kotlin
class Controller {
    private var clicks: Int = 0
    fun enableHook() {
        button.addMouseListener(object : MouseAdapter() {
            override fun mouseClicked(e: MouseEvent) {
                clicks++
            }
        })
    }
}
```

UI 버튼에 대한 참조가 있고 마우스 이벤트를 위해 enableHook 콜백을 추가했음을 짐작할 수 있다. 버튼을 클릭할 때마다 clicks 필드 값을 증가시킬 것이다.

### 데이터 클래스

데이터를 저장하기 위한 목적으로 클래스를 정의하는 경우는 빈번하게 발생한다. ; 스칼라의 케이스 클래스\(case class\)

kotlin에서는 데이터 클래스\(data class\)라는 이름으로 이와 유사한 개념을 제공한다.

```kotlin
data class Customer(val id: Int, val name: String, var address: String)
```

### 열거형 클래스



### 정적 메소드와 컴패니언 오브젝트 

## 인터페이스

## 상속

## 가시성 제어자

## 추상 클래스

## 인터페이스 또는 추상 클래스

## 다형성

## 오버라이딩 규칙

## 상속 대 합성

## 클래스 델리게이션

## 봉인 클래스

## 요약

