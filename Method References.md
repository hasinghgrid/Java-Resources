# Method References in Java

Method references in Java are a shorthand notation of a lambda expression to call a method directly. They make code more concise and readable by reusing existing methods without explicitly writing the lambda.

---

## 1. Static Method Reference

**Syntax:**

```java
ClassName::staticMethodName
```

**Example:**

```java
import java.util.function.Function;

public class StaticMethodRefExample {
    public static int square(int n) {
        return n * n;
    }

    public static void main(String[] args) {
        // Using Lambda
        Function<Integer, Integer> lambdaSquare = n -> StaticMethodRefExample.square(n);

        // Using Method Reference
        Function<Integer, Integer> methodRefSquare = StaticMethodRefExample::square;

        System.out.println(lambdaSquare.apply(5));  // 25
        System.out.println(methodRefSquare.apply(6)); // 36
    }
}
```

---

## 2. Instance Method Reference (Arbitrary Object of a Class)

**Syntax:**

```java
ClassName::instanceMethodName
```

Here, the method reference is applied to an **arbitrary object** of the class.

**Example:**

```java
import java.util.Arrays;
import java.util.List;

public class ArbitraryInstanceMethodRef {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("hardik", "singh", "java");

        // Using Lambda
        names.forEach(s -> System.out.println(s.toUpperCase()));

        // Using Method Reference
        names.forEach(String::toUpperCase); // won't print, just converts
        names.forEach(System.out::println); // prints each element
    }
}
```

---

## 3. Instance Method Reference (Particular Object)

**Syntax:**

```java
instance::methodName
```

Here, the method reference is tied to a **specific object instance**.

**Example:**

```java
import java.util.function.Consumer;

public class ParticularInstanceMethodRef {
    public static void main(String[] args) {
        // A particular object
        Consumer<String> lambdaPrinter = s -> System.out.println(s);

        // Using Method Reference
        Consumer<String> methodRefPrinter = System.out::println;

        lambdaPrinter.accept("Hello Lambda!");
        methodRefPrinter.accept("Hello Method Reference!");
    }
}
```

---

## 4. Constructor Reference

**Syntax:**

```java
ClassName::new
```

This is used when we want to create new objects using references.

**Example:**

```java
import java.util.function.Supplier;
import java.util.function.Function;
import java.util.ArrayList;

public class ConstructorRefExample {
    public static void main(String[] args) {
        // Using Lambda
        Supplier<ArrayList<String>> lambdaList = () -> new ArrayList<>();

        // Using Method Reference
        Supplier<ArrayList<String>> methodRefList = ArrayList::new;

        System.out.println(lambdaList.get()); // []
        System.out.println(methodRefList.get()); // []

        // Constructor with arguments
        Function<String, StringBuilder> builder = StringBuilder::new;
        System.out.println(builder.apply("Hello").append(" World")); // Hello World
    }
}
```

---

# Quick Comparison: Lambda vs Method Reference

| Type                                | Lambda Expression                            | Method Reference            |
| ----------------------------------- | -------------------------------------------- | --------------------------- |
| Static Method                       | `(n) -> ClassName.method(n)`                 | `ClassName::method`         |
| Instance Method (Arbitrary object)  | `(s) -> s.instanceMethod()`                  | `ClassName::instanceMethod` |
| Instance Method (Particular object) | `(x) -> instance.method(x)`                  | `instance::method`          |
| Constructor Reference               | `() -> new ClassName()` or `(x) -> new C(x)` | `ClassName::new`            |

---

# When to Use Method References

* When the lambda only calls an existing method.
* To make code **shorter, cleaner, and more readable**.
* They can replace many trivial lambdas in `Streams`, `Collectors`, and functional interfaces.

---
