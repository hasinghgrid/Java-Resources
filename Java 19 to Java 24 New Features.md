# Java 19 to Java 24 New Features

This document provides a detailed explanation of all major features introduced in **Java 19 to Java 24**, with examples, reasoning for introduction, and previous approaches or limitations.

---

## **Java 19 (September 2022)**

### 1. Virtual Threads (Preview)

**Issue:** Traditional Java threads are heavy, limiting scalability in applications with millions of concurrent tasks.

**Introduction:** Virtual threads are lightweight, allowing high concurrency with fewer resources.

**Example:**

```java
Thread.startVirtualThread(() -> System.out.println("Hello from virtual thread"));
```

### 2. Structured Concurrency (Incubator)

**Issue:** Managing multiple threads manually is error-prone and hard to reason about.

**Introduction:** Structured concurrency treats multiple tasks as a single unit for easier management and error handling.

**Example:**

```java
try (var scope = new StructuredTaskScope.ShutdownOnFailure()) {
    Future<String> user = scope.fork(() -> fetchUser());
    Future<String> orders = scope.fork(() -> fetchOrders());
    scope.join();
    System.out.println(user.resultNow() + orders.resultNow());
}
```

### 3. Record Patterns (Preview)

**Issue:** Pattern matching for records was limited and verbose.

**Example:**

```java
record Point(int x, int y) {}
Object obj = new Point(1, 2);
if (obj instanceof Point(int a, int b)) {
    System.out.println(a + b); // 3
}
```

### 4. Foreign Function & Memory API (Third Incubator)

**Reason:** Simplifies interaction with native code and off-heap memory safely.

**Example:**

```java
MemorySegment segment = MemorySegment.allocateNative(1024);
MemoryAccess.setIntAtOffset(segment, 0, 42);
System.out.println(MemoryAccess.getIntAtOffset(segment, 0));
```

---

## **Java 20 (March 2023)**

### 1. Virtual Threads (Second Preview)

*Enhancements for virtual threads, better API and performance.*

### 2. Scoped Values (Incubator)

**Issue:** Thread-local variables can be cumbersome and error-prone.

**Introduction:** Scoped values provide a structured way to pass immutable data across threads.

**Example:**

```java
ScopedValue<String> user = ScopedValue.newInstance();
try (ScopedValue.where(user, "Alice")) {
    System.out.println(ScopedValue.get(user)); // Alice
}
```

### 3. Pattern Matching for switch (Preview)

**Issue:** Switch statements are verbose and do not handle type patterns.

**Example:**

```java
Object obj = 42;
switch(obj) {
    case Integer i -> System.out.println("Integer: " + i);
    case String s -> System.out.println("String: " + s);
    default -> System.out.println("Unknown");
}
```

### 4. Record Patterns (Second Preview)

*Enhances destructuring capabilities in patterns.*

---

## **Java 21 (September 2023, LTS)**

### 1. Virtual Threads (Standard)

*Standardizes lightweight threads for high concurrency.*

### 2. Structured Concurrency (Second Incubator)

*Improves thread management, making concurrent code easier to write and reason about.*

### 3. Record Patterns (Third Preview)

*Further improvements to pattern matching with records.*

### 4. Pattern Matching for switch (Fifth Preview)

*Enhanced switch with type and record patterns.*

### 5. Sequenced Collections

**Issue:** Maintaining insertion order in sets and maps was verbose or required LinkedHash\* collections.

**Example:**

```java
SequencedSet<Integer> s = new LinkedHashSet<>();
s.add(3); s.add(1); s.add(2);
System.out.println(s); // [3,1,2]
```

### 6. String Templates (Preview)

**Issue:** String concatenation is verbose and error-prone.

**Example:**

```java
String name = "Alice";
String msg = STR."Hello, \{name}!";
System.out.println(msg); // Hello, Alice!
```

---

## **Java 22 (March 2024)**

### 1. Record Patterns (Second Preview)

*Continued enhancements for pattern matching and destructuring.*

### 2. Pattern Matching for switch (Sixth Preview)

*Further improvements on switch with patterns.*

### 3. Scoped Values (Second Preview)

*Enhances structured thread-local data management.*

### 4. Vector API (Seventh Incubator)

*Provides high-performance vector operations for SIMD computation.*

### 5. Stream Gatherers (Preview)

**Issue:** Existing stream collectors lacked composable aggregation methods.

**Example:**

```java
List<String> list = Stream.of("a","b","c").collect(Collectors.toList());
```

---

## **Java 23 (September 2024)**

### 1. Record Patterns (Third Preview)

*Further improvements to destructuring patterns.*

### 2. Pattern Matching for switch (Seventh Preview)

*Continued enhancements for type and record matching in switches.*

### 3. Scoped Values (Third Preview)

*Better structured management of immutable data across threads.*

### 4. Vector API (Eighth Incubator)

*Enhances performance-critical vector operations.*

### 5. Stream Gatherers (Second Preview)

*Enhances stream aggregation patterns.*

### 6. Module Import Declarations (Preview)

**Reason:** Simplifies module system import syntax.

**Example:**

```java
module my.module {
    import java.base;
}
```

---

## **Java 24 (March 2025)**

### 1. Ahead-of-Time Class Loading and Linking

**Reason:** Reduces JVM startup time.

### 2. Stream Gatherers (Enhanced)

*Further enhancements for parallel and composable stream operations.*

### 3. Permanently Disable the Security Manager

*Removes legacy security manager APIs.*

### 4. Primitive Types in Patterns, instanceof, and switch

**Example:**

```java
Object obj = 5;
if (obj instanceof Integer i) {
    System.out.println(i + 1); // 6
}
```

### 5. Flexible Constructor Bodies (Third Preview)

*Enhances expressiveness in constructors.*

### 6. Linking Run-Time Images without JMODs

*Improves runtime image creation.*

### 7. Module Import Declarations (Second Preview)

*Enhances module import declarations.*

### 8. Simple Source Files and Instance Main Methods (Fourth Preview)

*Simplifies Java file structure and entry points.*

### 9. Key Derivation Function API (Preview)

*Standard API for cryptography key derivation.*

### 10. Generational Shenandoah (Experimental)

*Improves garbage collection with generational ZGC.*

### 11. Compact Object Headers (Experimental)

*Reduces object memory overhead.*

### 12. ZGC: Remove the Non-Generational Mode

*Removes legacy GC mode for ZGC.*

### 13. Synchronize Virtual Threads without Pinning

*Improves virtual thread synchronization.*

### 14. Linking Run-Time Images without JMODs

*Further enhances runtime image linking.*
