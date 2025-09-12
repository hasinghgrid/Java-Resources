# Java 8 – Major Features, Why Introduced, and Examples

---

## 1. Lambda Expressions

* **Need**: Before Java 8, inline behaviors used **anonymous inner classes**, which were verbose and hard to read.
* **Feature**: Lambda expressions allow concise function-like expressions.
* **Example**:

  ```java
  List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

  // Before Java 8
  names.forEach(new Consumer<String>() {
      public void accept(String name) {
          System.out.println(name);
      }
  });

  // Java 8
  names.forEach(name -> System.out.println(name));
  ```
* **Benefit**: Cleaner code, enables functional programming style, integrates with Streams API.

---

## 2. Functional Interfaces & @FunctionalInterface

* **Need**: To clearly mark interfaces designed for lambda use (only **1 abstract method**).
* **Example**:

  ```java
  @FunctionalInterface
  interface Calculator {
      int compute(int a, int b);
  }

  Calculator add = (a, b) -> a + b;
  System.out.println(add.compute(5, 3)); // 8
  ```
* **Benefit**: Eliminates ambiguity, improves compiler checks.

---

## 3. Streams API

* **Need**: Iterating collections with loops was **verbose, error-prone, and not parallelizable easily**.
* **Feature**: Declarative, functional-style operations (filter, map, reduce, etc.) with parallel support.
* **Example**:

  ```java
  List<Integer> numbers = Arrays.asList(1,2,3,4,5);

  int sum = numbers.stream()
                   .filter(n -> n % 2 == 0)
                   .mapToInt(Integer::intValue)
                   .sum();

  System.out.println(sum); // 6
  ```
* **Benefit**: Less boilerplate, parallel execution possible with `.parallelStream()`.

---

## 4. Default & Static Methods in Interfaces

* **Need**: Adding new methods to interfaces earlier broke existing implementations.
* **Feature**: Interfaces can have `default` and `static` methods.
* **Example**:

  ```java
  interface Vehicle {
      default void start() {
          System.out.println("Starting vehicle");
      }
      static void info() {
          System.out.println("Vehicle interface");
      }
  }
  ```
* **Benefit**: Backward compatibility, evolving APIs without breaking old code.

---

## 5. Optional Class

* **Need**: To avoid **NullPointerException** and reduce null checks.
* **Example**:

  ```java
  Optional<String> name = Optional.ofNullable(null);
  System.out.println(name.orElse("Unknown")); // Unknown
  ```
* **Benefit**: More expressive null handling.

---

## 6. New Date/Time API (`java.time`)

* **Need**: Old `Date` and `Calendar` were **mutable, inconsistent, and not thread-safe**.
* **Example**:

  ```java
  LocalDate today = LocalDate.now();
  LocalDate nextWeek = today.plusWeeks(1);
  System.out.println(nextWeek);
  ```
* **Benefit**: Immutable, thread-safe, ISO standard-based API.

---

## 7. Method References

* **Need**: Reduce redundancy in lambda expressions.
* **Example**:

  ```java
  List<String> names = Arrays.asList("Alice", "Bob");
  names.forEach(System.out::println);
  ```
* **Benefit**: Cleaner syntax when method already exists.

---

## 8. Nashorn JavaScript Engine *(removed later)*

* **Need**: Integrate Java with JavaScript for scripting inside JVM.
* **Example**:

  ```java
  ScriptEngineManager manager = new ScriptEngineManager();
  ScriptEngine engine = manager.getEngineByName("nashorn");
  engine.eval("print('Hello from JS')");
  ```
* **Benefit**: JVM polyglot capability.

---

## 9. Repeating Annotations

* **Need**: Earlier, annotations couldn’t repeat on the same element.
* **Example**:

  ```java
  @Repeatable(Hints.class)
  @interface Hint { String value(); }

  @interface Hints { Hint[] value(); }

  @Hint("hint1")
  @Hint("hint2")
  class Person {}
  ```
* **Benefit**: Cleaner metadata, avoids container annotations.

---

## ✅ Summary of Java 8

Java 8 was a **revolutionary release** — introduced **functional programming (lambdas, streams, functional interfaces)**, modern APIs (`Optional`, new Date/Time), and improved backward compatibility (`default` methods).
