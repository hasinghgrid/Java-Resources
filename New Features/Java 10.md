# Java 10 – Major Features, Why Introduced, and Examples

---

## 1. Local-Variable Type Inference (`var`)

* **Need**: Declaring local variables with explicit types was sometimes verbose and redundant when the type was obvious.
* **Feature**: Introduced `var` for type inference in local variables.
* **Example**:

  ```java
  var message = "Hello, Java 10!"; // inferred as String
  var numbers = List.of(1, 2, 3);   // inferred as List<Integer>
  ```
* **Benefit**: Cleaner, more concise code without losing type safety.

---

## 2. Application Class-Data Sharing (AppCDS)

* **Need**: JVM startup time and memory usage were concerns for large applications.
* **Feature**: AppCDS allows **sharing of common class metadata** across different JVM instances.
* **Benefit**: Faster startup, reduced memory footprint, especially useful in cloud and microservice environments.

---

## 3. Parallel Full GC for G1

* **Need**: G1 Garbage Collector’s full GC was single-threaded and caused long pause times.
* **Feature**: Parallelized full GC in G1 to improve performance.
* **Benefit**: Reduced pause times, better scalability for applications with large heaps.

---

## ✅ Summary of Java 10

Java 10 was a **short-term release** focusing on **developer productivity (`var`)** and **JVM performance (AppCDS, G1 GC improvements)**. It streamlined everyday coding while also optimizing runtime behavior.
