# Java 18 Features

Java 18 (released in March 2022) introduced several new language features, API enhancements, and performance improvements.

---

## 1. Simple Web Server

**Purpose:** Provide a minimal HTTP server for prototyping and testing.

**Example:**

```bash
# Start a simple server in current directory on port 8080
java -m jdk.httpserver 8080
```

**Advantages:**

* Quick prototyping without external frameworks.
* Lightweight, zero-configuration server.

**Earlier Alternative:**

* Setting up Jetty, Tomcat, or using `com.sun.net.httpserver` manually in code.

---

## 2. Code Snippets in Java API Documentation

**Purpose:** Allow developers to include interactive code snippets in Javadoc.

**Example:**

```java
/**
 * Example usage:
 * <pre>{@code
 * List<String> list = List.of("A", "B");
 * list.forEach(System.out::println);
 * }</pre>
 */
```

**Advantages:**

* Clearer, runnable examples in documentation.
* Improves learning and adoption.

**Earlier Alternative:**

* Manual text examples without execution.

---

## 3. UTF-8 by Default

**Purpose:** Use UTF-8 as the default charset for standard APIs.

**Advantages:**

* Consistency across platforms.
* Reduces charset-related bugs.

**Earlier Alternative:**

* Explicitly specifying charset `StandardCharsets.UTF_8` in code.

---

## 4. Vector API (Incubator)

**Purpose:** High-performance vector computations using SIMD instructions.

**Example:**

```java
var vectorA = IntVector.fromArray(IntVector.SPECIES_128, new int[]{1,2,3,4}, 0);
var vectorB = IntVector.fromArray(IntVector.SPECIES_128, new int[]{5,6,7,8}, 0);
var result = vectorA.add(vectorB);
```

**Advantages:**

* Hardware-accelerated computations.
* Improved performance for numerical applications.

**Earlier Alternative:**

* Manual loops over arrays or using libraries like Apache Commons Math.

---

## 5. Foreign Function & Memory API (Second Incubator)

**Purpose:** Interact with native code safely, continued improvement from Java 17.

**Advantages:**

* Safer than JNI.
* Cleaner syntax, better performance.

---

### Summary Table

| Feature                  | Advantage                    | Prior Alternative                 |
| ------------------------ | ---------------------------- | --------------------------------- |
| Simple Web Server        | Lightweight HTTP prototyping | Jetty/Tomcat or manual HTTPServer |
| Code Snippets in Javadoc | Clear runnable examples      | Manual examples                   |
| UTF-8 Default            | Platform consistency         | Explicit charset specification    |
| Vector API               | SIMD performance             | Manual loops or libraries         |
| Foreign Function API     | Safe native calls            | JNI                               |
