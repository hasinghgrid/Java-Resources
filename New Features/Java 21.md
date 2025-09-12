# 🌟 Java 21 Features

Java 21 (LTS, released in September 2023) brings exciting updates with focus on productivity, performance, and modern language features.

---

## 🧵 1. Virtual Threads (Finalized)

**✨ Purpose:**

* Lightweight threads for highly concurrent applications.

**💡 Example:**

```java
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    executor.submit(() -> System.out.println("Hello from virtual thread!"));
}
```

**✅ Advantages:**

* Handle millions of concurrent tasks easily.
* Simplifies code for high-concurrency applications.

**⚠️ Earlier Alternative:**

* Traditional `Thread` objects or thread pools.

---

## 🔄 2. Structured Concurrency (Incubator)

**✨ Purpose:**

* Manage multiple tasks as a single unit for better error handling and structured lifecycle.

**💡 Example:**

```java
try (var scope = new StructuredTaskScope.ShutdownOnFailure()) {
    Future<String> f1 = scope.fork(() -> fetchDataA());
    Future<String> f2 = scope.fork(() -> fetchDataB());
    scope.join();
    System.out.println(f1.resultNow() + " " + f2.resultNow());
}
```

**✅ Advantages:**

* Reduces boilerplate for managing multiple concurrent tasks.
* Easier exception propagation and handling.

**⚠️ Earlier Alternative:**

* Manual thread management with `Future` objects.

---

## 🔍 3. Record Patterns

**✨ Purpose:**

* Simplify destructuring of record objects in `if` or `switch` statements.

**💡 Example:**

```java
record Point(int x, int y) {}

Point p = new Point(7, 14);
if (p instanceof Point(int a, int b)) {
    System.out.println("X: " + a + ", Y: " + b);
}
```

**✅ Advantages:**

* Cleaner and readable code for extracting fields.

**⚠️ Earlier Alternative:**

* Manual getter calls.

---

## ⚡ 4. Pattern Matching for `switch`

**✨ Purpose:**

* Type-safe and concise multi-branch logic combining pattern matching with `switch` expressions.

**💡 Example:**

```java
Object obj = new Point(3, 4);
switch(obj) {
    case Point(int x, int y) -> System.out.println("X: " + x + ", Y: " + y);
    default -> System.out.println("Unknown type");
}
```

**✅ Advantages:**

* Expressive and safe multi-branch statements.

**⚠️ Earlier Alternative:**

* Nested `if-else` with type checks and casting.

---

## 🌐 5. Foreign Function & Memory API

**✨ Purpose:**

* Interact safely with native code with improved API.

**✅ Advantages:**

* Cleaner than JNI.
* Safer and performant.

---

### 📊 Summary Table

| Feature                     | Advantages                                     | Earlier Alternative                |
| --------------------------- | ---------------------------------------------- | ---------------------------------- |
| 🧵 Virtual Threads          | Millions of lightweight threads                | Traditional threads / thread pools |
| 🔄 Structured Concurrency   | Unified task management, easier error handling | Manual thread/Future coordination  |
| 🔍 Record Patterns          | Cleaner destructuring                          | Getter calls                       |
| ⚡ Pattern Matching `switch` | Type-safe multi-branch logic                   | Nested if-else + casting           |
| 🌐 Foreign Function API     | Safe and performant native interop             | JNI                                |
