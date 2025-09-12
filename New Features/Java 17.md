# Java 17 Features

Java 17 (LTS, released in September 2021) introduces a mix of new language features, library enhancements, and JVM improvements.

---

## 1. Sealed Classes

**Purpose:** Restrict which classes can extend or implement a class/interface.

**Example:**

```java
public sealed class Vehicle permits Car, Bike { }

public final class Car extends Vehicle { }

public non-sealed class Bike extends Vehicle { }
```

**Advantages:**

* Clearly defines inheritance boundaries.
* Enables better pattern matching in `switch`.
* Enhances maintainability and security.

**Earlier Alternative:**

* Documentation-based restrictions.
* Package-private constructors or final classes.

---

## 2. Pattern Matching for `instanceof`

**Purpose:** Simplify type checks and casting.

**Example:**

```java
Object obj = "Hello, Java 17";

if (obj instanceof String s) {
    System.out.println(s.toUpperCase());
}
```

**Earlier Alternative:**

```java
if (obj instanceof String) {
    String s = (String) obj;
    System.out.println(s.toUpperCase());
}
```

---

## 3. Switch Expressions (Standardized)

**Purpose:** Use `switch` as an expression returning a value.

**Example:**

```java
int day = 2;
String dayName = switch(day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    default -> "Other";
};
System.out.println(dayName); // Tuesday
```

**Earlier Alternative:**

```java
String dayName;
switch(day) {
    case 1: dayName = "Monday"; break;
    case 2: dayName = "Tuesday"; break;
    default: dayName = "Other";
}
```

---

## 4. Text Blocks (Multiline Strings)

**Purpose:** Simplify multiline string literals.

**Example:**

```java
String json = """
{
    "name": "John",
    "age": 30
}
""";
System.out.println(json);
```

**Earlier Alternative:**

```java
String json = "{\n" +
              "  \"name\": \"John\",\n" +
              "  \"age\": 30\n" +
              "}";
```

---

## 5. Stream.toList() Method

**Purpose:** Collect a Stream into an unmodifiable list.

**Example:**

```java
List<Integer> numbers = Stream.of(1,2,3,4).toList();
System.out.println(numbers);
```

**Earlier Alternative:**

```java
List<Integer> numbers = Stream.of(1,2,3,4)
                              .collect(Collectors.toList());
```

---

## 6. Foreign Function & Memory API (Incubator)

**Purpose:** Interact with native code without JNI.

**Example:**

```java
MemorySegment segment = MemorySegment.allocateNative(100);
```

**Earlier Alternative:**

* JNI (verbose, error-prone)

---

## 7. New RandomGenerator Interface & Implementations

**Example:**

```java
RandomGenerator rng = RandomGenerator.of("L32X64MixRandom");
System.out.println(rng.nextInt());
```

**Earlier Alternative:**

```java
Random random = new Random();
System.out.println(random.nextInt());
```

---

## 8. Strongly Encapsulated JDK Internals

**Purpose:** Enforce module boundaries for internal APIs.

**Earlier Alternative:**

* Accessing internal classes with `--illegal-access` flag.

---

## 9. Enhanced Pseudo-Random Number Generators (PRNG)

**Example:**

```java
RandomGenerator rng = RandomGenerator.of("Xoshiro256PlusPlus");
int randNum = rng.nextInt();
```

**Earlier Alternative:**

* `java.util.Random` (limited and legacy algorithms)

---

### Summary Table

| Feature                       | Advantage                   | Prior Alternative              |
| ----------------------------- | --------------------------- | ------------------------------ |
| Sealed classes                | Control inheritance         | Documentation, package-private |
| Pattern matching `instanceof` | Cleaner casting             | Manual casting                 |
| Switch expressions            | Returns value, less verbose | Traditional switch + breaks    |
| Text blocks                   | Multiline strings           | String concatenation           |
| Stream.toList()               | Cleaner stream collection   | Collectors.toList()            |
| Foreign Function API          | Safer native calls          | JNI                            |
| RandomGenerator               | More RNG algorithms         | java.util.Random               |
| Strong encapsulation          | Security, maintainability   | `--illegal-access`             |
