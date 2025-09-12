# Java 12 – Major Features, Why Introduced, and Examples

---

## 1. Switch Expressions (Preview)

* **Need**: Traditional `switch` statements were verbose and couldn’t be used as expressions.
* **Feature**: `switch` can now return values and use concise syntax.
* **Example**:

  ```java
  int day = 3;
  String type = switch (day) {
      case 1, 7 -> "Weekend";
      default -> "Weekday";
  };
  ```
* **Benefit**: Cleaner, less error-prone, allows expression-style coding.

---

## 2. Compact Number Formatting

* **Need**: Formatting numbers into compact, human-readable forms required custom logic.
* **Feature**: Added `NumberFormat.getCompactNumberInstance`.
* **Example**:

  ```java
  NumberFormat nf = NumberFormat.getCompactNumberInstance(Locale.US, NumberFormat.Style.SHORT);
  System.out.println(nf.format(1000)); // 1K
  ```
* **Benefit**: Easier internationalization and user-friendly formatting.

---

## 3. JVM Constants API

* **Need**: No standard way to model and access class-file and runtime constants.
* **Feature**: Introduced `java.lang.invoke.constant` API to describe constants.
* **Benefit**: Easier manipulation of constants for tools and frameworks.

---

## 4. G1 Garbage Collector Improvements

* **Need**: G1 GC sometimes had unpredictable pause times and inefficiencies.
* **Feature**: Improvements such as **abortable mixed collections** and better pause predictability.
* **Benefit**: More stable performance for large-scale applications.

---

## ✅ Summary of Java 12

Java 12 focused on **developer productivity (switch expressions, compact number formatting)** and **runtime improvements (JVM constants API, G1 GC tuning)**. It continued simplifying Java code while improving JVM performance.
