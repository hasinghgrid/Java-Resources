# Java 8 to Java 13 New Features

This document provides a detailed explanation of all major features introduced in **Java 8 to Java 13**, with examples, reasoning for introduction, and previous approaches or limitations.

---

## **Java 8 (March 2014)**

### 1. Lambda Expressions

**Issue:** Java previously relied on anonymous inner classes for inline behavior, which were verbose.

**Introduction:** Lambda expressions provide a concise way to represent functional interfaces.

**Example:**

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.forEach(name -> System.out.println(name));
```

*Before Java 8:*

```java
names.forEach(new Consumer<String>() {
    public void accept(String name) {
        System.out.println(name);
    }
});
```

### 2. Functional Interfaces and @FunctionalInterface

**Reason:** To clearly define interfaces intended for lambda expressions.

**Example:**

```java
@FunctionalInterface
interface Calculator {
    int compute(int a, int b);
}
Calculator add = (a, b) -> a + b;
System.out.println(add.compute(5, 3));
```

### 3. Streams API

**Issue:** Processing collections required verbose loops.

**Introduction:** Provides declarative and functional operations on sequences.

**Example:**

```java
List<Integer> numbers = Arrays.asList(1,2,3,4,5);
int sum = numbers.stream()
                 .filter(n -> n % 2 == 0)
                 .mapToInt(Integer::intValue)
                 .sum();
System.out.println(sum); // Output: 6
```

### 4. Default and Static Methods in Interfaces

**Issue:** Adding methods to interfaces would break existing implementations.

**Example:**

```java
interface Vehicle {
    default void start() {
        System.out.println("Starting vehicle");
    }
    static void info() {
        System.out.println("Vehicle interface");
    }
}
```

### 5. Optional Class

**Issue:** NullPointerExceptions were common and required verbose null checks.

**Example:**

```java
Optional<String> name = Optional.ofNullable(null);
System.out.println(name.orElse("Unknown")); // Output: Unknown
```

### 6. New Date/Time API (java.time)

**Issue:** `java.util.Date` and `Calendar` were mutable, non-thread-safe, and inconsistent.

**Example:**

```java
LocalDate today = LocalDate.now();
LocalDate nextWeek = today.plusWeeks(1);
System.out.println(nextWeek);
```

### 7. Method References

**Example:**

```java
List<String> names = Arrays.asList("Alice", "Bob");
names.forEach(System.out::println);
```

### 8. Nashorn JavaScript Engine

**Reason:** Integrate Java and JavaScript in JVM easily.

**Example:**

```java
ScriptEngineManager manager = new ScriptEngineManager();
ScriptEngine engine = manager.getEngineByName("nashorn");
engine.eval("print('Hello from JS')");
```

### 9. Repeating Annotations

**Issue:** Previously, annotations could not be repeated on the same element.

**Example:**

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Repeatable(Hints.class)
@interface Hint { String value(); }
@interface Hints { Hint[] value(); }

@Hint("hint1")
@Hint("hint2")
class Person {}
```

---

## **Java 9 (September 2017)**

### 1. Java Platform Module System (JPMS)

**Issue:** Large applications had dependency and encapsulation issues.

**Example:**

```java
module my.module {
    requires java.base;
}
```

*Allows strong encapsulation and modularization.*

### 2. JShell (REPL)

**Reason:** Previously, testing Java code snippets required creating a class and `main` method.

**Example:**

```bash
jshell> int x = 5;
jshell> x + 2
```

### 3. Collection Factory Methods

**Issue:** Creating immutable collections was verbose.

**Example:**

```java
List<String> list = List.of("A", "B", "C");
Set<String> set = Set.of("X", "Y");
Map<String, Integer> map = Map.of("a",1, "b",2);
```

### 4. Private Interface Methods

**Reason:** Reduce code duplication in interfaces.

**Example:**

```java
interface Calculator {
    private static int square(int x) { return x*x; }
    static int sumOfSquares(int a, int b) { return square(a) + square(b); }
}
```

### 5. Stream API Enhancements

```java
List<Integer> numbers = List.of(1,2,3,4,5);
numbers.stream().takeWhile(n -> n<4).forEach(System.out::println); // 1,2,3
numbers.stream().dropWhile(n -> n<3).forEach(System.out::println); // 3,4,5
Stream.ofNullable(null).forEach(System.out::println); // nothing printed
```

### 6. Process API Improvements

```java
ProcessHandle current = ProcessHandle.current();
System.out.println(current.pid());
```

*Simplifies process management.*

### 7. Multi-Release JAR Files

*Allows a single JAR to contain bytecode for multiple Java versions.*

### 8. Stack-Walking API

*More efficient and flexible alternative to `Thread.getStackTrace()`.*

### 9. Compact Strings

*Reduces memory footprint for strings that only contain Latin-1 characters.*

---

## **Java 10 (March 2018)**

### 1. Local-Variable Type Inference (`var`)

**Issue:** Explicit type declaration is verbose for local variables.

**Example:**

```java
var message = "Hello, Java 10!"; // inferred as String
var numbers = List.of(1,2,3); // inferred as List<Integer>
```

### 2. Application Class-Data Sharing (AppCDS)

*Improves JVM startup and reduces memory footprint by sharing class metadata.*

### 3. Parallel Full GC for G1

*Improves garbage collection performance.*

---

## **Java 11 (September 2018)**

### 1. HTTP Client API

**Issue:** `HttpURLConnection` was cumbersome.

**Example:**

```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder()
        .uri(URI.create("https://example.com"))
        .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());
```

### 2. String Methods

```java
String s = " Hello ";
System.out.println(s.isBlank()); // false
System.out.println(s.strip());   // "Hello"
System.out.println("a\nb".lines().toList()); // [a,b]
System.out.println("ha".repeat(3)); // hahaha
```

### 3. Local-Variable Syntax for Lambda Parameters

```java
(var x, var y) -> x + y
```

### 4. Flight Recorder (JFR)

*Previously commercial; now available in JDK for profiling.*

### 5. Removal/Deprecation of Some Modules

*Java EE, CORBA removed to reduce footprint.*

### 6. Nest-Based Access Control

*Allows nested classes to access private members efficiently.*

---

## **Java 12 (March 2019)**

### 1. Switch Expressions (Preview)

**Issue:** Switch statements were verbose and lacked expressions.

**Example:**

```java
int day = 3;
String type = switch(day) {
    case 1, 7 -> "Weekend";
    default -> "Weekday";
};
```

### 2. Compact Number Formatting

```java
NumberFormat nf = NumberFormat.getCompactNumberInstance(Locale.US, NumberFormat.Style.SHORT);
System.out.println(nf.format(1000)); // 1K
```

### 3. JVM Constants API

*Provides a programmatic way to describe class-file constants.*

### 4. G1 Improvements

*Improved GC pause predictability and abortable mixed collections.*

---

## **Java 13 (September 2019)**

### 1. Text Blocks (Preview)

**Issue:** Multi-line strings required `
` and string concatenation.

**Example:**

```java
String html = """
<html>
  <body>Hello</body>
</html>
""";
```

*Improves readability for multi-line strings.*

### 2. Switch Expressions (Second Preview)

*Continued enhancements of switch expressions.*

### 3. Reimplement Legacy Socket API

*Better error handling and performance.*

### 4. Dynamic CDS Archives

\*Improves startup by generating class-data sharing archives dynamica
