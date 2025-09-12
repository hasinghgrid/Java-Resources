# Java 14 – Major Features, Why Introduced, and Examples

---

## 1. Records (Preview)

* **Need**: Writing simple data carrier classes required a lot of boilerplate (constructors, getters, `equals`, `hashCode`, `toString`).
* **Feature**: `record` keyword introduced for concise immutable data classes.
* **Example**:

  ```java
  record Point(int x, int y) {}

  Point p = new Point(5, 10);
  System.out.println(p.x()); // 5
  ```
* **Benefit**: Automatically provides boilerplate code, reduces errors, and makes intent clear.

---

## 2. Pattern Matching for `instanceof` (Preview)

* **Need**: After using `instanceof`, explicit casting was always required.
* **Feature**: Pattern matching allows binding the type directly.
* **Example**:

  ```java
  Object obj = "Hello";
  if (obj instanceof String s) {
      System.out.println(s.toUpperCase());
  }
  ```
* **Benefit**: Reduces redundancy and improves readability.

---

## 3. Helpful NullPointerExceptions

* **Need**: Standard NPE messages didn’t show which variable was null, making debugging hard.
* **Feature**: JVM now provides more descriptive NPE messages.
* **Example**:

  ```java
  String s = null;
  s.length(); // JVM message: "Cannot invoke \"String.length()\" because \"s\" is null"
  ```
* **Benefit**: Easier debugging and faster resolution of errors.

---

## 4. Switch Expressions (Standardized)

* **Need**: After being previewed in Java 12 and 13, switch expressions were ready for production.
* **Feature**: `switch` expressions became a standard feature.
* **Example**:

  ```java
  int day = 2;
  String type = switch (day) {
      case 1, 7 -> "Weekend";
      default -> "Weekday";
  };
  ```
* **Benefit**: More powerful and concise switch usage.

---

## 5. Foreign-Memory Access API (Incubator)

* **Need**: Accessing off-heap/native memory was unsafe and complex with `sun.misc.Unsafe`.
* **Feature**: Introduced Foreign-Memory Access API with `MemorySegment` and `MemoryAddress`.
* **Benefit**: Safer and more efficient memory access outside the JVM heap.

---

## 6. JFR Event Streaming

* **Need**: Java Flight Recorder (JFR) profiling was static and lacked real-time streaming.
* **Feature**: Event streaming API added for real-time JVM monitoring.
* **Benefit**: Better observability and diagnostics in production.

---

## ✅ Summary of Java 14

Java 14 introduced **big productivity enhancements (records, pattern matching, helpful NPEs, switch expressions)** and **runtime improvements (foreign memory access, JFR streaming)**, marking a step toward more modern, concise, and safer Java.
