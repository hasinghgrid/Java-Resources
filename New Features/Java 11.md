# Java 11 – Major Features, Why Introduced, and Examples

---

## 1. HTTP Client API

* **Need**: The old `HttpURLConnection` API was cumbersome and outdated.
* **Feature**: New modern HTTP Client API supporting **HTTP/1.1** and **HTTP/2**.
* **Example**:

  ```java
  HttpClient client = HttpClient.newHttpClient();
  HttpRequest request = HttpRequest.newBuilder()
      .uri(URI.create("https://example.com"))
      .build();

  HttpResponse<String> response = client.send(request,
      HttpResponse.BodyHandlers.ofString());

  System.out.println(response.body());
  ```
* **Benefit**: Simplifies HTTP calls, supports async and reactive communication.

---

## 2. New String Methods

* **Need**: Common string operations (blank checks, trimming, repetition) required verbose code.
* **Feature**: Added several utility methods.
* **Example**:

  ```java
  String s = " Hello ";
  System.out.println(s.isBlank());      // false
  System.out.println(s.strip());        // "Hello"
  System.out.println("a\nb".lines().toList()); // [a, b]
  System.out.println("ha".repeat(3));   // hahaha
  ```
* **Benefit**: Cleaner, built-in solutions for everyday tasks.

---

## 3. Local-Variable Syntax for Lambda Parameters

* **Need**: To allow consistent use of `var` in lambda expressions.
* **Feature**: Now `var` can be used in lambda parameter declarations.
* **Example**:

  ```java
  (var x, var y) -> x + y
  ```
* **Benefit**: Improves readability and enables annotations on lambda parameters.

---

## 4. Flight Recorder (JFR)

* **Need**: Profiling and monitoring were limited to commercial tools.
* **Feature**: JFR, previously commercial-only, became open source in Java 11.
* **Benefit**: Efficient, low-overhead monitoring and profiling for production systems.

---

## 5. Removal/Deprecation of Some Modules

* **Need**: Java EE modules (like JAXB, JAX-WS, CORBA) were outdated and rarely used.
* **Feature**: These were **removed or deprecated** to simplify the JDK.
* **Benefit**: Smaller, cleaner, more maintainable core JDK.

---

## 6. Nest-Based Access Control

* **Need**: Nested classes accessing private members required synthetic bridge methods.
* **Feature**: Nest-based access allows direct access between nested classes.
* **Benefit**: More efficient and secure handling of nested class relationships.

---

## ✅ Summary of Java 11

Java 11 (LTS) brought **modern APIs (HTTP Client, String utilities)**, **developer-friendly syntax (var in lambdas)**, and **runtime improvements (JFR, nest-based access)**. It also removed legacy Java EE/CORBA modules, streamlining the JDK for modern development.
