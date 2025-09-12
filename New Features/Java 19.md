# Java 19 Features

Java 19 (released in September 2022) introduced several preview and incubator features aimed at improving productivity, performance, and modern programming paradigms.

---

## 1. Virtual Threads (Preview)

**Purpose:** Lightweight threads for high-concurrency applications.

**Example:**

```java
ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor();
executor.submit(() -> System.out.println("Hello from a virtual thread"));
executor.shutdown();
```

**Advantages:**

* Millions of threads without memory overhead.
* Simplifies writing highly concurrent applications.

**Earlier Alternative:**

* Traditional `Thread` objects or thread pools.

---

## 2. Structured Concurrency (Incubator)

**Purpose:** Manage multiple tasks as a single unit of work.

**Example:**

```java
var scope = new StructuredTaskScope.ShutdownOnFailure();
scope.fork(() -> fetchDataFromServiceA());
scope.fork(() -> fetchDataFromServiceB());
scope.join();
```

**Advantages:**

* Easier error handling across tasks.
* Reduces boilerplate for managing multiple threads.

**Earlier Alternative:**

* Manual thread management and `Future` coordination.

---

## 3. Record Patterns (Preview)

**Purpose:** Simplify destructuring of record objects in `switch` and pattern matching.

**Example:**

```java
record Point(int x, int y) {}

Point p = new Point(10, 20);
if (p instanceof Point(int a, int b)) {
    System.out.println(a + ", " + b);
}
```

**Advantages:**

* Cleaner code for extracting values from immutable records.

**Earlier Alternative:**

* Manual getter calls.

---

## 4. Pattern Matching for `switch` (Preview)

**Purpose:** Combine pattern matching with `switch` expressions.

**Example:**

```java
Object obj = new Point(1, 2);
switch(obj) {
    case Point(int x, int y) -> System.out.println(x + ", " + y);
    default -> System.out.println("Unknown");
}
```

**Advantages:**

* More expressive and type-safe multi-branch logic.

**Earlier Alternative:**

* Nested `if-else` with type checks and casting.

---

## 5. Foreign Function & Memory API (Third Incubator)

**Purpose:** Continue enhancing native interop introduced in Java 17/18.

**Advantages:**

* Safer and easier interaction with native libraries.

---

### Summary Table

| Feature                   | Advantage                       | Prior Alternative                  |
| ------------------------- | ------------------------------- | ---------------------------------- |
| Virtual Threads           | Millions of lightweight threads | Traditional threads / thread pools |
| Structured Concurrency    | Unified task management         | Manual thread/Future coordination  |
| Record Patterns           | Cleaner destructuring           | Getter calls                       |
| Pattern Matching `switch` | Expressive, type-safe branching | Nested if-else + casting           |
| Foreign Function API      | Safe native interop             | JNI                                |
