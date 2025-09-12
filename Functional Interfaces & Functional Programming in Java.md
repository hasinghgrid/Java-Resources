# 🌿 Functional Interfaces & Functional Programming in Java (Cheat Sheet)

---

## 🔹 What is Functional Programming (FP)?

* **Programming paradigm** where computation is expressed as evaluation of functions.
* Focuses on **what to do** rather than **how to do it**.
* Encourages **immutability**, **statelessness**, and **function composition**.
* Java supports **hybrid FP** (not purely functional).

---

## 🔹 Functional Interfaces

A **Functional Interface** = interface with exactly **1 abstract method** (SAM – Single Abstract Method).

* Used in **Lambdas** and **Method References**.
* Can also have **default** and **static** methods.

```java
@FunctionalInterface
interface Calculator {
    int operate(int a, int b);
}
```

---

## 🔹 Built-in Functional Interfaces (java.util.function)

### 1. **Consumer Family** – takes input, returns nothing

| Interface         | Method Signature        | Example                                                                 |
| ----------------- | ----------------------- | ----------------------------------------------------------------------- |
| `Consumer<T>`     | `void accept(T t)`      | `Consumer<String> printer = s -> System.out.println(s);`                |
| `BiConsumer<T,U>` | `void accept(T t, U u)` | `BiConsumer<String,Integer> disp = (n,a)->System.out.println(n+":"+a);` |
| `IntConsumer`     | `void accept(int v)`    | `IntConsumer ic = x -> System.out.println(x*2);`                        |

---

### 2. **Supplier Family** – provides value, no input

| Interface     | Method Signature | Example                                        |
| ------------- | ---------------- | ---------------------------------------------- |
| `Supplier<T>` | `T get()`        | `Supplier<Double> rand = () -> Math.random();` |

---

### 3. **Function Family** – takes input, returns output

| Interface           | Method Signature    | Example                                                 |
| ------------------- | ------------------- | ------------------------------------------------------- |
| `Function<T,R>`     | `R apply(T t)`      | `Function<String,Integer> len = s -> s.length();`       |
| `BiFunction<T,U,R>` | `R apply(T t, U u)` | `BiFunction<Integer,Integer,Integer> add = (a,b)->a+b;` |
| `UnaryOperator<T>`  | `T apply(T t)`      | `UnaryOperator<Integer> sq = x -> x*x;`                 |
| `BinaryOperator<T>` | `T apply(T t, T u)` | `BinaryOperator<Integer> max = Integer::max;`           |

---

### 4. **Predicate Family** – tests condition, returns boolean

| Interface          | Method Signature        | Example                                                     |
| ------------------ | ----------------------- | ----------------------------------------------------------- |
| `Predicate<T>`     | `boolean test(T t)`     | `Predicate<Integer> even = n -> n%2==0;`                    |
| `BiPredicate<T,U>` | `boolean test(T t,U u)` | `BiPredicate<String,Integer> longer = (s,n)->s.length()>n;` |

---

## 🔹 Method References

Shorthand for lambdas that just call methods.

1. **Static** → `ClassName::staticMethod`

```java
Function<String,Integer> parser = Integer::parseInt;
```

2. **Instance (particular object)** → `instance::method`

```java
Consumer<String> printer = System.out::println;
```

3. **Instance (arbitrary object of a type)** → `ClassName::method`

```java
Function<String,String> upper = String::toUpperCase;
```

4. **Constructor** → `ClassName::new`

```java
Supplier<List<String>> listSupplier = ArrayList::new;
```

---

## 🔹 Streams + Functional Interfaces

Streams use functional interfaces:

* `filter(Predicate<T>)`
* `map(Function<T,R>)`
* `forEach(Consumer<T>)`
* `reduce(BinaryOperator<T>)`

```java
List<String> names = Arrays.asList("John", "Maya", "Hardik");

names.stream()
     .filter(s -> s.startsWith("H")) // Predicate
     .map(String::toUpperCase)       // Function
     .forEach(System.out::println);  // Consumer
```

---

## 🔹 Optional

```java
Optional<String> name = Optional.ofNullable("Hardik");
name.ifPresent(System.out::println);  // Consumer
String result = name.orElseGet(() -> "Default"); // Supplier
```

---

## 🔹 Advantages

* ✅ Concise, expressive, less boilerplate.
* ✅ Encourages immutability → fewer bugs.
* ✅ Easy parallelism with Streams.
* ✅ Declarative style (focus on *what*, not *how*).
* ✅ Functions are composable & testable.

---

## 🔹 When to Use / Avoid

**Use When:**

* Data processing pipelines (filter, map, reduce).
* Callbacks, event handling.
* Concurrency with `CompletableFuture`, `parallelStream`.

**Avoid When:**

* Performance-critical loops (lambda overhead).
* Heavy mutable state.
* Complex recursion (no tail-call optimization).

---

## 🔹 Data Structures Best with FP

* **Collections (List, Set, Map)** → perfect with Streams.
* **Concurrent Collections** (e.g., ConcurrentHashMap) with `computeIfAbsent`, `merge`.
* **Immutable Collections** (Java 9+: `List.of()`, `Map.of()`).
* **Arrays** with `Arrays.stream()`.
* **Optional** for null-safety.

---

## 🔹 Complete Example

```java
import java.util.*;
import java.util.function.*;

public class FunctionalDemo {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("John", "Maya", "Hardik", "Meera");

        Predicate<String> startsWithM = s -> s.startsWith("M");
        Function<String, Integer> length = String::length;
        Consumer<String> printer = System.out::println;
        Supplier<Date> now = Date::new;

        names.stream()
             .filter(startsWithM)   // Predicate
             .map(length.andThen(Object::toString)) // Function
             .forEach(printer);     // Consumer

        System.out.println("Current Date: " + now.get());
    }
}
```

---

✅ This cheat sheet covers **all major functional interfaces, method references, usage in Streams/Optional, advantages, best practices, and examples**.
