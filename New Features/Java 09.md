# Java 9 – Major Features, Why Introduced, and Examples

---

## 1. Java Platform Module System (JPMS)

* **Need**: Large applications suffered from **dependency management issues** and lack of **encapsulation**. Everything was accessible via classpath.
* **Feature**: Introduced **modules** for strong encapsulation and reliable configuration.
* **Example**:

  ```java
  module my.module {
      requires java.base;
  }
  ```
* **Benefit**: Better modularization, secure APIs, improved maintainability.

---

## 2. JShell (REPL)

* **Need**: Testing Java code required writing a full class with `main` method.
* **Feature**: JShell provides an interactive **Read-Eval-Print-Loop (REPL)**.
* **Example**:

  ```
  jshell> int x = 5;
  jshell> x + 2
  $2 ==> 7
  ```
* **Benefit**: Faster experimentation, learning, and prototyping.

---

## 3. Collection Factory Methods

* **Need**: Creating immutable collections was verbose and required multiple lines.
* **Feature**: Added concise factory methods.
* **Example**:

  ```java
  List<String> list = List.of("A", "B", "C");
  Set<String> set = Set.of("X", "Y");
  Map<String, Integer> map = Map.of("a",1, "b",2);
  ```
* **Benefit**: Clean, concise, and immutable by default.

---

## 4. Private Interface Methods

* **Need**: Interfaces had `default` methods but code duplication could not be avoided inside them.
* **Feature**: Now `private` methods can be used inside interfaces to share logic.
* **Example**:

  ```java
  interface Calculator {
      private static int square(int x) { return x * x; }
      static int sumOfSquares(int a, int b) { return square(a) + square(b); }
  }
  ```
* **Benefit**: Better code reuse within interfaces.

---

## 5. Stream API Enhancements

* **Need**: Some operations like early termination or null-safe streams were missing.
* **Feature**: Added `takeWhile`, `dropWhile`, and `Stream.ofNullable`.
* **Example**:

  ```java
  List<Integer> numbers = List.of(1,2,3,4,5);
  numbers.stream().takeWhile(n -> n < 4).forEach(System.out::println); // 1,2,3
  numbers.stream().dropWhile(n -> n < 3).forEach(System.out::println); // 3,4,5
  Stream.ofNullable(null).forEach(System.out::println); // prints nothing
  ```
* **Benefit**: More expressive and safer stream operations.

---

## 6. Process API Improvements

* **Need**: Managing processes via `Runtime.exec` was cumbersome.
* **Feature**: New `ProcessHandle` API to interact with OS processes.
* **Example**:

  ```java
  ProcessHandle current = ProcessHandle.current();
  System.out.println(current.pid());
  ```
* **Benefit**: Simpler and more powerful process management.

---

## 7. Multi-Release JAR Files

* **Need**: Library developers struggled to support multiple Java versions.
* **Feature**: A single JAR can contain version-specific class files.
* **Benefit**: Backward compatibility across different JDK versions.

---

## 8. Stack-Walking API

* **Need**: `Thread.getStackTrace()` was inefficient and limited.
* **Feature**: New `StackWalker` API provides efficient, lazy stack trace access.
* **Benefit**: Better debugging and profiling.

---

## 9. Compact Strings

* **Need**: `String` used UTF-16 internally, wasting memory for Latin-1 data.
* **Feature**: Compact Strings store characters more efficiently.
* **Benefit**: Reduced memory footprint, especially in large applications.

---

## ✅ Summary of Java 9

Java 9 focused on **modularity (JPMS)**, **developer productivity (JShell, factory methods)**, **API enhancements (streams, process API)**, and **performance (compact strings, stack walking)** — paving the way for modern scalable Java applications.
