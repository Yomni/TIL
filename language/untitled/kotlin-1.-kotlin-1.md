---
description: Hello World!
---

# \[Kotlin 후려치기\] 1. Kotlin 시작하기

### Kotlin 컴파일 및 실행

### 사전준비

* openJDK 및 jenv 설치
* Kotlin 설치

```bash
# MacOS 에서 Homebrew를 이용하여 kotlin 설치
$ brew update
$ brew install kotlin
```

### Hello world 코드 작성

```kotlin
// HelloWorld.kt
/* static 같은 키워드는 사용하지 않아도 된다.
 * 
 */

fun main(args: Array<String>) {
    println("Hello, World!")
}
```

### Compile을 통해 jar 어셈블리 생성

```bash
$ kotlinc HelloWorld.kt -include-runtime -d HelloWorld.jar
```

### java 명령어를 통해 jar파일 프로그램 실행

```bash
$ java -jar HelloWorld.jar 
# Hello, World!
```

### .class\(바이트코드\) 로 컴파일하기

```bash
# HelloWorldkt.class 파일이 생성된다(바이트코드)
$ kotlinc HelloWorld.kt
```

### javap로 바이트코드 분석

```bash
# Kotlin으로 바이트 코드를 생성하여도, 결국 JVM에 의해 해석되어야 하므로
# java 코드 컴파일 결과와 동일한 class 파일을 생성한다.
Compiled from "HelloWorld.kt"
public final class HelloWorldKt {
  public static final void main(java.lang.String[]);
    Code:
       0: aload_0
       1: ldc           #9                  // String args
       3: invokestatic  #15                 // Method kotlin/jvm/internal/Intrinsics.checkNotNullParameter:(Ljava/lang/Object;Ljava/lang/String;)V
       6: ldc           #17                 // String Hello, World!
       8: astore_1
       9: iconst_0
      10: istore_2
      11: getstatic     #23                 // Field java/lang/System.out:Ljava/io/PrintStream;
      14: aload_1
      15: invokevirtual #29                 // Method java/io/PrintStream.println:(Ljava/lang/Object;)V
      18: return
}
```

### Kotlin 런타임

Hello, World! 를 컴파일하고 jar를 생성할 때, 명령어 중 kotlin runtime을 포함하도록 지시했다.

`-include-runtime` : 객체 타입이 널 값이 아님을 검증하기 위한 메소드를 호출하기 때문에 런타임을 포함하지 않고 컴파일일 하고 실행하려 할 경우 예외가 발생한다.

* Kotlin은 런타임에서 객체의 널 값이 아닌지 반드시 검사한다.
* Java 라이브러리와는 다르다.
* 결과물인 jar에 이를 합치거나 클래스 경로에 이를 제공해야만 한다.

```bash
$ kotlinc HelloWorld.kt -d HelloWorld.jar
$ java -jar HelloWorld.jar 
Exception in thread "main" java.lang.NoClassDefFoundError: kotlin/jvm/internal/Intrinsics
	at HelloWorldKt.main(HelloWorld.kt)
Caused by: java.lang.ClassNotFoundException: kotlin.jvm.internal.Intrinsics
	at java.base/jdk.internal.loader.BuiltinClassLoader.loadClass(BuiltinClassLoader.java:581)
	at java.base/jdk.internal.loader.ClassLoaders$AppClassLoader.loadClass(ClassLoaders.java:178)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:522)
	... 1 more
# null 값이 아님을 검증하기 위한 메소드를 호출하면서 예외가 발생한다
```

### 요약

* 코틀린 코드를 빌드하고 실행하는 데 필요한 도구와 개발 환경 구축

