# Java 14 to Java 18 New Features

This document provides a detailed explanation of all major features introduced in **Java 14 to Java 18**, with examples, reasoning for introduction, and previous approaches or limitations.

---

## **Java 14 (March 2020)**

### 1. Records (Preview)

**Issue:** Previously, creating simple immutable data classes required verbose boilerplate code.

**Introduction:** Records provide a concise way to declare immutable data carriers.

**Example:**

```java
record Point(int x, int y) {}
Point p = new Point(5, 10);
System.out.println(p.x()); // 5
```

*Automatically provides `equals`, `hashCode`, and `toString`.*

### 2. Pattern Matching for instanceof (Preview)

**Issue:** Type casting after `instanceof` was repetitive.

**Example:**

```java
Object obj = "Hello";
if(obj instanceof String s) {
    System.out.println(s.toUpperCase());
}
```

*Simplifies type checks and casts.*

### 3. Helpful NullPointerExceptions

**Reason:** NullPointerExceptions were hard to debug.

**Example:**

```java
String s = null;
s.length(); // JVM shows exactly which variable was null
```

### 4. Switch Expressions (Standardized)

**Example:**

```java
int day = 2;
String type = switch(day) {
    case 1, 7 -> "Weekend";
    default -> "Weekday";
};
```

### 5. Foreign-Memory Access API (Incubator)

**Reason:** Efficient memory access outside the Java heap.

**Example:**

```java
// Use MemorySegment, MemoryAddress to access off-heap memory
```

### 6. JFR Event Streaming

*Real-time monitoring of JVM events.*

---

## **Java 15 (September 2020)**

### 1. Text Blocks (Standard)

*Simplifies multi-line string literals.*

```java
String html = """
<html>
  <body>Hello</body>
</html>
""";
```

### 2. Sealed Classes (Preview)

**Issue:** Previously, restricting subclassing required documentation and runtime checks.

**Example:**

```java
sealed interface Shape permits Circle, Rectangle {}
final class Circle implements Shape {}
non-sealed class Rectangle implements Shape {}
```

*Restricts which classes can extend or implement a type.*

### 3. Hidden Classes

*Allows frameworks to define classes dynamically without polluting the public API.*

### 4. Records (Second Preview)

*Enhancements and fixes to record features.*

### 5. Foreign-Memory Access API (Second Incubator)

*Further improvements for off-heap memory access.*

### 6. ZGC Improvements

*Reduces pause times and improves memory management.*

---

## **Java 16 (March 2021)**

### 1. Records (Standard)

*Records are now a standard feature.*

```java
record Employee(String name, int id) {}
```

### 2. Pattern Matching for instanceof (Standard)

*No longer preview; simplifies type checks.*

### 3. Stream.toList()

**Example:**

```java
List<Integer> list = Stream.of(1,2,3).toList();
```

*Simpler conversion from stream to list.*

### 4. Sealed Classes (Second Preview)

*Continued development of sealed classes.*

### 5. Vector API (Incubator)

**Reason:** Efficient SIMD operations for performance-critical code.

### 6. Foreign Linker API (Incubator)

*Simplifies calling native libraries.*

### 7. Strong Encapsulation of JDK Internals

*Encourages proper API usage, reduces internal dependency hacks.*

---

## **Java 17 (September 2021, LTS)**

### 1. Sealed Classes (Standard)

*Final standardization of sealed classes.*

### 2. Pattern Matching for switch (Preview)

**Example:**

```java
Object obj = "Hello";
switch(obj) {
    case String s -> System.out.println(s.length());
    default -> System.out.println("Unknown");
}
```

### 3. New Pseudo-Random Number Generators (PRNG)

**Example:**

```java
RandomGenerator rnd = RandomGenerator.of("L64X128MixRandom");
int num = rnd.nextInt(100);
```

### 4. jpackage Tool

*Create native installers for Java applications.*

### 5. Foreign Function & Memory API (Incubator)

*Enhances JVM support for off-heap memory and native calls.*

### 6. Deprecations & Removals

*Applets, RMI Activation, and older APIs removed.*

---

## **Java 18 (March 2022)**

### 1. Simple Web Server

**Reason:** Quickly run small HTTP servers for testing.

**Example:**

```bash
java -m jdk.httpserver 8000
```

### 2. UTF-8 by Default

*All charset operations default to UTF-8, simplifying internationalization.*

### 3. Vector API (Second Incubator)

*Enhancements to SIMD operations for high-performance code.*

### 4. Code Snippets in API Documentation

*Allows adding executable code snippets to Javadoc.*

### 5. Pattern Matching for switch (Second Preview)

*Continued improvements on switch pattern matching.*

### 6. Foreign Function & Memory API (Second Incubator)

*Further refinements for off-heap memory and native function access.*
