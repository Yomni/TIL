---
description: '고차 함수, 람다식, 객체 지향 프로그래밍 언어 로서의 코틀린의 특성'
---

# \[Kotlin 후려치기\] 3. Kotlin 과 객체 지향 프로그래밍\(Object - Oriented Programming\)

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

열거형 클래스의 구체적인 타입으로, 주어진 enum 타입 변수는 미리 정의된 상수로 제한된다. 상수는 타입에 의해 정의되어 있다.

```kotlin
// 일반적인 enum 타입 클래스
enum class Day { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY }

// 생성자를 매개변수로 가지는 enum 타입 클래스 
// 일종의 Planet 이름을 Key, (mass, radius)를 value로 가지는 Map 
enum class Planet(val mass: Double, val radius: Double) {
    MERCURY(3.303e+23, 2.4397e6), VENUS(4.869e+24, 6.0518e6)
}

// 사용하기 위해선 다음과 같이 사용한다
Planet.valueOf("MERCURY") // MERCURY
Planet.valueOf("MERCURY").mass // 3.303e+23
Planet.valueOf("MERCURY").radius // 2.4397e6
// 정의한 모든 값을 얻는 방법
Planet.values() // Array<Planet> return

// enum과 interface 를 익명으로 구현할 수 있다
public enum class Word : Printable {
    HELLO {
        override fun print() {
            println("Word is HELLO")
        }
    },
    BYE {
        override fun print() {
            println("Word is BYE")
        }
    }
}

val w = Word.HELLO
w.print()
```

### 정적 메소드와 컴패니언 오브젝트 

* 코틀린은 자바와 달리 클래스를 위한 정적 메소드를 지원하지 않는다
* 정적 메소드는 객체 인스턴스에 속해 있는 것이 아니라, 타입 자신에 속해 있다\(객체를 만들지 않고도 사용 가능하다\)
* 코틀린에서 정적 메소드 기능을 구현하기 위해서는 메소드를 패키지 레벨에 정의하는 것이 바람직하다 \(파일을 Static 으로 명명\)

```kotlin
fun showFirstCharacter(input: String): Char {
    if(input.isEmpty()) throw IllegalAccessException()
    return input.first()
}

// static method 처럼 사용 할 수 있다
showFirstCharacter("Test String") // T
```

이런 소스의 사용이 가능하게 하는 메커니즘의 핵심은 다음과 같다.

* 컴파일러는 실제로 public final 의 키워드를 가지는 클래스를 패키지.파일명으로 생성한다.
* 정의한 메소드를 컴파일러가 생성한 클래스의 static 메소드로 추가한다.
* 특히, [invokestatic](https://stackoverflow.com/questions/34360718/invokestatic-on-static-method-in-interface) 루틴을 통해 만들어진다.

이런 특징을 이용해서 싱글톤 패턴을 쉽게 정의할 수 있다.

```kotlin
object Sigleton {
    private var count = 0
    fun doSomething(): Unit {
        println("Calling a doSomething (${++count} call/-s in total)")
    }
}
```

* 위 코드는 모든 함수에서 Singleton.doSomething 메소드를 호출할 수 있다
* 호출할 때마다 카운터 값이 증가한다.
* 컴파일러는 내부적으로 위 코드를 public final 클래스로 생성한다
* INSTANCE라고 부르는 멤버를 하나 도입하고 이를 static으로 지정한다.
* 특히, static{} 코드를 임의로 추가하며, 이는 초기화\(initializer\)로 오직 한 번만 호출되며, 다음과 같은 동작 전에 static{} 코드 부분이 먼저 호출된다.
  * 클래스 인스턴스 생성
  * 클래스 정적 메소드 호출
  * 클래스 정적 필드에 값 할당
  * 비상수\(non-constant\) 정적 필드 사용
  * 최상위 클래스를 위해 클래스 내부에서 어휘적으로 중첩된 assert 문 실행

코틀린에서도 자바에서 호출하는 것처럼 정적 메소드를 호출하는 방법이 있다. 이를 위해, 객체를 클래스 안에 위치시킨 다음 이를 컴패니언 오브젝트\(companion object\)로 지정해야 한다. 

```kotlin
interface StudentFactory {
    fun create(name:String): Student
}

class Student private constructor(val name: String) {
    // 일종의 static method를 호출하는 방법
    companion object : StudentFactory {
        override fun create(name: String): Student {
            return Student(name)
        }
    }
}
```

* Student 타입의 생성자는 private로 지정되어 있음
  * 생성자는 Student 클래스 내부나 companion object를 제외한 어느 곳에서도 생성자를 호출할 수 없다
* companion 클래스는 Student의 모든 메소드와 멤버에 접근할 수 있다. 

## 인터페이스

* 연관된 기능의 집합에 대한 정의 ; 일종의 계약
* 인터페이스를 구현하는 쪽은 약속된 인터페이스를 준수하고 필요한 메소드를 반드시 구현해야 한다
* 추상 메소드를 선언 / 메소드 구현체 를 가질 수 있다
* **상태는 가질 수 없으나, 프로퍼티는 가질 수 있다\(추상 클래스와의 차이\)**

```kotlin
interface Document {
    // 프로퍼티 
    val version: Long
    val size: Long
    
    // 프로퍼티 이지만 기본 구현 제공
    val name: String
    get() = "NoName"
    
    fun save(input: InputStream)
    fun load(stream: OutputStream)
    // 기본 구현
    fun getDescription(): String {return "Document $name has $size byte(-s)"}
}


class DocumentImpl : Document {
    override val size : Long
    get() = 0
    
    override fun load(stream: OutputStream) {
        
    }
    
    override fun save(input: InputStream) {
        
    }
    
    override val version: Long
    get() = 0
    
}
```

## 상속\(Inheritance\)

_**객체지향 프로그래밍의 핵심 중 하나**_

* 기존 클래스를 재활용 또는 확장해 행위를 수정한 새로운 클래스를 생성
* 이 때, 기존 클래스를 슈퍼 클래스\(또는 부모 클래스\), 새로 생성한 클래스를 파생된\(derived\) 클래스라 부른다
* 슈퍼클래스는의 상속은 한 번만 가능, 인터페이스는 여러 개 상속 가능
* C가 B로부터 파생된 클래스이고, B는 A로부터 파생된 클래스라면, C는 A로 부터 파생된 클래스이다\(~~삼단 논법~~\)
* 슈퍼 클래스의 모든 필드와 프로퍼티를 받게 된다

### 상속의 의의

* 재사용성 극대화 \(슈퍼클래스의 필드와 프로퍼티를 모두 받을 수 있으므로\)
* 상속을 통한 파생된 클래스의 전문화 \(슈퍼 클래스에 비해 좀 더 세분화 되고 확장된 개념으로 정의\) 

## 가시성 제어자

* public : 모든 곳에서 접근 가능
* internal : 모듈 코드에서만 접근 가능
* protected : 정의한 클래스 및 파생된 클래스에서만 접근 가능
* private : 정의한 클래스 스코프 내에서만 접근할 수 있음

## 추상 클래스

_**derived class가 공유하는 공통된 메소드 및 프로퍼티 집합을 제공하기 위한 부분적으로 정의된 클래스  
ex\) InputStream 클래스**_

* 클래스 정의부 앞에 `abstract` 키워드를 추가하여 정의 가능 
* 구현부가 없는 프로퍼티와 메소드는 파생된 클래스에서 반드시 구현
* 추상 클래스는 인스턴스를 생성할 수 없음

```kotlin
abstract class A {
    // derived class에서 반드시 구현
    abstract fun doSomething()
}
```

## 인터페이스 vs 추상 클래스

* Is-a : 'B는 A 이다.'의 관계가 성립하지 않는다면, 인터페이스로 구현
* Can-Do : 인터페이스는 Can-Do 관계를 의미한다

ex\) OutputStream : 추상 클래스, FileOutputStream, ByteOutputStream : 파생된 클래스  
Autocloseable : interface

## 다형성\(Polymorphism\)

캡슐화, 상속에 이어 객체 지향 프로그래밍의 세번째 특징 ; 타입 단계에서 '어떻게'로부터 '무엇을'을 분리한다.

_**한 타입의 참조 변수로 여러 타입의 객체를 참조할 수 있도록 한다.**_  
따라서 다음과 같은 식의 코딩이 가능하다.

```kotlin
// Ellipsis / Rectangle 모두 Shape 라는 클래스를 상속하고 있다고 가정
fun main(args: Array<String>) {
    val e1 = Ellipsis()
    e1.Height = 10
    e1.Width = 12
    
	val e2 = Ellipsis()
    e2.Height = 100
    e2.Width = 96

    val r1 = Rectangle()
    r1.XLocation = 49
    r1.YLocation = 45
    r1.Width = 10
    r1.Height = 10
    
    val shapes = listOf<Shape>(e1,e2,r1)
    // 각각의 실제 구현체에 따라 isHit 내부의 로직이 다르게 동작할 수 있다.
    // 다형성을 통해 이는 shape의 참조 변수로만 접근하면 된다.
    val selected:Shape? = shapes.firstOrNull{ shape -> shape.isHit(50,52) }
}
```

## 오버라이딩 규칙

오버라이딩\(overriding\) : 새로운 클래스에서 부모 클래스로부터 상속받은 메소드 중 재정의 하는 것

코틀린은 일반적으로 자바보다 더 명시적인 언어이고, 자바에서 모든 메소드는 기본적으로 가상 메소드이다. 그러므로 모든 파생된 클래스에서는 오버라이딩 할 수 있다.  
반면에 코틀린에서는 함수를 재정의하기 위해 함수가 오버라이딩에 대해 열려\(open\)있다는 것을 표시해야 한다. 이를 위해 메소드 정의부에 접두사로 `open` 키워드를 추가해야 하며, 메소드를 재정의할 때에는 꼭 `override` 키워드를 메소드에 표시해야 한다

```kotlin
abstract class SingleEngineAirplane protected constructor() {
    abstract fun fly()
}

class CesnaAirplane : SingleEngineAirplane() {
    /*
     * 메소드 앞에 final 키워드를 추가하면 파생된 클래스에서 오버라이딩 하는 것을
     * 항상 허용하지 않도록 할수 있다.
     */
    final override fun fly() {
        println("Flying a cesna")
    }
}
```

* 함수에만 국한된 것이 아니라 프로퍼티도 가상으로 표시할 수 있고, 오버라이딩 할 수 있다

```kotlin
open class Base {
    open val property1: String
        get() = "Base::value"
}

class Derived1 : Base() {
    override val property1: String
        get() = "Derived::value"
}

class Derived2(override val property1: String) : Base() {}
```

* val 프로퍼티를 var로도 오버라이딩할 수 있지만, 역은 성립하지 않는다

```kotlin
open class BaseB(open val propertyFoo:String) {
}

class DerivedB : BaseB("") {
    private var _propFoo: String = ""
    override var propertyFoo: String
        get() = _propFoo
        set(value) {
            _propFoo = value
        }
}
```

```kotlin
// interface, abstract class 동시적용
open class Image {
    open fun save(output: OutputStream) {
        println("Some logic to save an image")
    }
}

interface VendorImage {
    fun save(output: OutputStream) {
        println("Vendor saving an image")
    }
}

class PNGImage : Image(), VendorImage{
    override fun save(output: OutputStream) {
        super<VendorImage>.save(output)
        super<Image>.save(output)
    }
}

fun main(args: Array<String>) {
    val pngImage = PNGImage()
    val os = ByteArrayOutputStream()
    pngImage.save(os)
}
```

## 상속 대 합성



## 클래스 델리게이션

## 봉인 클래스

## 요약

