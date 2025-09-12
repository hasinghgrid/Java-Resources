# Java 13 – Major Features, Why Introduced, and Examples

---

## 1. Text Blocks (Preview)

* **Need**: Writing multi-line strings required lots of escapes and concatenations, making code messy.
* **Feature**: Introduced **text blocks** using `"""` for multi-line strings.
* **Example**:

  ```java
  String html = """
      <html>
        <body>Hello</body>
      </html>
      """;
  ```
* **Benefit**: Improves readability, easier to write SQL, JSON, XML, and HTML inline.

---

## 2. Switch Expressions (Second Preview)

* **Need**: Further refinement after feedback from Java 12’s preview.
* **Feature**: Enhanced syntax and semantics for `switch` expressions.
* **Example**:

  ```java
  int day = 5;
  String type = switch (day) {
      case 1, 7 -> "Weekend";
      default -> "Weekday";
  };
  ```
* **Benefit**: Moves closer to standardization, reduces verbosity.

---

## 3. Reimplement Legacy Socket API

* **Need**: The old Socket API was outdated, hard to maintain, and had inconsistent behavior.
* **Feature**: Reimplemented on a modern, maintainable foundation.
* **Benefit**: Better performance, reliability, and error handling in networking applications.

---

## 4. Dynamic CDS Archives

* **Need**: Class Data Sharing (CDS) archives had to be created manually before.
* **Feature**: JDK can now create **dynamic CDS archives** at application execution.
* **Benefit**: Faster startup times without manual intervention.

---

## ✅ Summary of Java 13

Java 13 focused on **developer productivity (text blocks, switch refinements)** and **JVM/runtime improvements (socket reimplementation, dynamic CDS archives)**, continuing the path toward more readable code and optimized performance.
