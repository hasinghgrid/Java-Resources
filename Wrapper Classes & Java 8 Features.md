# 📘 Wrapper Classes & Java 8 Features in Java

This guide explains **where and why wrapper classes are used** in Java, and highlights the **major features introduced in Java 8** with practical examples.

---

## 🔹 Wrapper Classes in Java

Wrapper classes are used whenever objects are required instead of primitives.

### ✅ 1. Java Collections

Collections cannot store primitives, only objects.

```java
List<Integer> list = new ArrayList<>();
list.add(10); // autoboxing: int → Integer
int val = list.get(0); // unboxing: Integer → int
```

### ✅ 2. Generics

Generics only work with objects.

```java
public class Box<T> {
    T value;
}

Box<Integer> intBox = new Box<>(); // int wouldn’t work
```

### ✅ 3. Nullability

Primitives can’t hold `null`, wrappers can.

```java
Integer age = null; // allowed, unlike int
```

### ✅ 4. Utility Methods

Built-in parsing and conversion methods.

```java
int n = Integer.parseInt("123");
double d = Double.parseDouble("3.14");
boolean b = Boolean.parseBoolean("true");
```

### ✅ 5. Streams & Lambdas

Wrapper types are required in Stream API.

```java
List<Integer> numbers = List.of(1, 2, 3);
numbers.stream().map(n -> n * 2).forEach(System.out::println);
```

### ✅ 6. Comparisons & Sorting

Wrappers implement `Comparable`.

```java
List<Integer> nums = Arrays.asList(10, 5, 20);
Collections.sort(nums); // uses Integer.compareTo
```

### ✅ 7. Annotations & Reflection

Frameworks prefer wrappers.

```java
public class User {
    private Integer id;
    private Boolean active;
}
```

### ✅ 8. Multithreading & Atomic Types

Wrappers in concurrent utilities.

```java
AtomicInteger counter = new AtomicInteger(0);
counter.incrementAndGet();
```

### 🔄 Summary Table

| Use Case                | Why Wrapper is Used               |
| ----------------------- | --------------------------------- |
| Collections (List, Map) | Only accept objects               |
| Generics                | Only support objects              |
| Nullability             | Primitives can’t be null          |
| Parsing                 | Static methods in wrapper classes |
| Lambda & Streams        | Work with object types            |
| Frameworks              | Reflection, annotations           |
| Multithreading          | Thread-safe atomic wrappers       |

---

## 🚀 Java 8 Features

Java 8 introduced **functional programming** and **performance improvements**.

### ✅ 1. Lambda Expressions

```java
// Before Java 8
Collections.sort(list, new Comparator<String>() {
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
});

// Java 8
list.sort((a, b) -> a.compareTo(b));
```

**Use Case:** Sorting, event handling, iteration.

### ✅ 2. Functional Interfaces

```java
@FunctionalInterface
interface Calculator {
    int operate(int a, int b);
}

Calculator add = (a, b) -> a + b;
System.out.println(add.operate(2, 3)); // 5
```

**Common ones:** `Predicate<T>`, `Function<T,R>`, `Consumer<T>`, `Supplier<T>`

### ✅ 3. Stream API

```java
List<String> names = List.of("Ram", "Shyam", "Mohan");

names.stream()
    .filter(name -> name.startsWith("S"))
    .map(String::toUpperCase)
    .forEach(System.out::println);
```

**Use Case:** Efficient bulk operations.

### ✅ 4. Method References

```java
names.forEach(System.out::println);
```

**Types of Method References:**

1. Static → `ClassName::staticMethod`
2. Instance (specific object) → `object::method`
3. Instance (arbitrary object) → `Class::method`
4. Constructor → `Class::new`

#### Example

```java
class Utils {
    static void print(String s) { System.out.println(s); }
}

List<String> names = List.of("A", "B", "C");
names.forEach(Utils::print); // static reference
```

### ✅ 5. Default Methods in Interfaces

```java
interface Vehicle {
    default void start() {
        System.out.println("Starting...");
    }
}
```

**Use Case:** Backward compatibility.

### ✅ 6. Optional<T>

```java
Optional<String> name = Optional.ofNullable(getName());
name.ifPresent(System.out::println);
```

**Use Case:** Avoid `NullPointerException`.

---

## 🔁 Lambda vs Method Reference

```java
// Lambda
list.forEach(s -> System.out.println(s));

// Method Reference
list.forEach(System.out::println);
```

✅ Method references are **cleaner** when reusing existing methods.

---

## 📌 Conclusion

* **Wrapper Classes** → Bridge between primitives and objects. Essential for collections, generics, null handling, concurrency, and frameworks.
* **Java 8 Features** → Ushered functional programming in Java (Lambdas, Streams, Method References, Optional, Default Methods).

👉 Together, they enable modern, robust, and cleaner Java code.
