# Functional Programming, Method References, Streams, Wrapper Classes, and Generics in Java

---

## 🔹 1. Functional Programming (FP)

### What is FP?

Functional Programming is a **programming paradigm** where computation is expressed as the evaluation of **mathematical functions**. It avoids mutable data and state changes, instead emphasizing **pure functions** and **declarative programming**.

### Why is it called *Functional*?

It’s called so because **functions are the primary building blocks**, treated as first-class citizens (can be passed around like variables).

* **Mathematics analogy**: `f(x) = x * 2` always gives the same result for the same input.
* In FP: Functions are expected to be **pure** and **side-effect free**.

### Key Concepts in FP

1. **Pure Functions**

```java
int square(int x) { return x * x; } // always same output for same input
```

2. **Immutability**

```java
List<Integer> newList = oldList.stream()
                               .map(n -> n + 1)
                               .toList();
```

3. **First-Class & Higher-Order Functions**

```java
Function<Integer, Integer> doubler = x -> x * 2;
Stream.of(1, 2, 3).map(doubler).forEach(System.out::println);
```

4. **Function Composition**

```java
Function<Integer, Integer> multiply2 = x -> x * 2;
Function<Integer, Integer> add3 = x -> x + 3;
Function<Integer, Integer> combined = multiply2.andThen(add3);
System.out.println(combined.apply(5)); // 13
```

5. **Declarative Programming**

```java
List<Integer> evenSquares = nums.stream()
                                .filter(n -> n % 2 == 0)
                                .map(n -> n * n)
                                .toList();
```

6. **Referential Transparency**

```java
int x = 2 * 5;  // always 10
```

7. **Lazy Evaluation**

```java
Stream<Integer> s = Stream.of(1, 2, 3, 4).filter(n -> n > 2);
System.out.println(s.findFirst().get()); // only evaluates needed elements
```

8. **Recursion instead of loops**

```java
int factorial(int n) {
    return (n == 0) ? 1 : n * factorial(n - 1);
}
```

9. **Monads & Optional**

```java
Optional<String> name = Optional.of("Java");
name.map(String::toUpperCase).ifPresent(System.out::println);
```

10. **No Side Effects**

```java
// Avoid modifying external state, keep functions independent
```

---

## 🔹 2. Method References

Method Reference = shorthand for lambdas that only call an existing method.

### Syntax

```
ClassName::methodName
objectRef::methodName
ClassName::new   // constructor reference
```

### Types with Examples

#### 1. Static Method Reference

```java
List<Integer> numbers = Arrays.asList(5, 3, 8, 1);
numbers.forEach(System.out::println);
```

#### 2. Instance Method (Particular Object)

```java
class Printer {
    void printMessage(String msg) { System.out.println(msg); }
}
Printer p = new Printer();
List<String> list = Arrays.asList("Hello", "World");
list.forEach(p::printMessage);
```

#### 3. Instance Method (Arbitrary Object)

```java
List<String> names = Arrays.asList("java", "python", "cpp");
names.sort(String::compareToIgnoreCase);
```

#### 4. Constructor Reference

```java
Supplier<StringBuilder> supplier = StringBuilder::new;
System.out.println(supplier.get().append("Created via constructor reference"));
```

---

## 🔹 3. Streams Example

Streams = sequence of elements supporting functional operations.

```java
List<Integer> nums = Arrays.asList(2, 5, 7, 8, 10);

int result = nums.stream()
                 .filter(n -> n % 2 == 0)   // keep evens
                 .map(n -> n * n)           // square
                 .reduce(0, Integer::sum);  // sum

System.out.println("Sum = " + result); // 168
```

---

## 🔹 4. Wrapper Classes

Wrapper classes convert primitives into objects.

| Primitive | Wrapper   |
| --------- | --------- |
| int       | Integer   |
| char      | Character |
| double    | Double    |
| boolean   | Boolean   |

### Example

```java
int primitive = 10;
Integer obj = primitive;   // Autoboxing
int value = obj;           // Unboxing

System.out.println("Wrapper object = " + obj);
System.out.println("Unboxed value = " + value);
```

---

## 🔹 5. Generics

Generics = write **type-safe reusable code**.

### Generic Class

```java
class Box<T> {
    private T value;
    public void set(T value) { this.value = value; }
    public T get() { return value; }
}

Box<String> strBox = new Box<>();
strBox.set("Hello");
System.out.println(strBox.get());

Box<Integer> intBox = new Box<>();
intBox.set(100);
System.out.println(intBox.get());
```

### Generic Method

```java
class Utils {
    public static <T> void printArray(T[] arr) {
        for (T t : arr) System.out.print(t + " ");
        System.out.println();
    }
}

Integer[] intArr = {1, 2, 3};
String[] strArr = {"A", "B", "C"};
Utils.printArray(intArr);
Utils.printArray(strArr);
```

---

## ✅ Summary

* **Functional Programming** → pure functions, immutability, declarative style.
* **Method References** → shorthand for lambdas (`System.out::println`).
* **Streams** → functional-style collection processing.
* **Wrapper Classes** → object forms of primitives.
* **Generics** → reusable type-safe classes & methods.
