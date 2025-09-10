# Java Streams API - Complete Guide

## 1. Why Streams Came into Java

Before Java 8, handling collections often required **external iteration** (using loops or iterators). This led to verbose, error-prone code. For example:

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
List<String> result = new ArrayList<>();
for (String name : names) {
    if (name.startsWith("A")) {
        result.add(name.toUpperCase());
    }
}
```

This was repetitive, hard to parallelize, and not very readable.

**Streams** (introduced in Java 8) solved this by providing a **functional, declarative style** of programming. They allow developers to focus on **what** to do rather than **how** to do it.

---

## 2. What is a Stream?

* A **Stream** is a sequence of elements supporting **sequential** and **parallel** aggregate operations.
* It does **not store data** but works on data from collections, arrays, or I/O channels.
* It is **lazy**: intermediate operations are not executed until a terminal operation is invoked.

---

## 3. When and Where to Use Streams

✅ Use Streams when:

* You need to **process collections** (filtering, mapping, reducing).
* You want **cleaner, declarative code** instead of loops.
* You want to take advantage of **parallelism** (using `.parallelStream()`).

❌ Avoid Streams when:

* The logic is very simple (plain `for` loop might be clearer).
* You need **indexed access** (Streams don’t work well with random access).
* Performance overhead of Streams is unnecessary (tight loops in performance-critical code).

---

## 4. Stream Workflow

1. **Source** → Collection, Array, File, etc.
2. **Intermediate Operations** (lazy, return Stream) → map, filter, sorted, etc.
3. **Terminal Operations** (eager, consume Stream) → collect, forEach, reduce, etc.

---

## 5. Stream Intermediate Operations (Lazy)

| Operation | Description                      | Example                                        |
| --------- | -------------------------------- | ---------------------------------------------- |
| map       | Transform each element           | `list.stream().map(String::toUpperCase)`       |
| filter    | Keep elements matching predicate | `list.stream().filter(s -> s.startsWith("A"))` |
| flatMap   | Flatten nested streams           | `nested.stream().flatMap(List::stream)`        |
| distinct  | Remove duplicates                | `list.stream().distinct()`                     |
| sorted    | Sort elements                    | `list.stream().sorted()`                       |
| peek      | Debug/inspect elements           | `list.stream().peek(System.out::println)`      |
| limit     | Take first N elements            | `list.stream().limit(3)`                       |
| skip      | Skip first N elements            | `list.stream().skip(2)`                        |

---

## 6. Stream Terminal Operations (Eager)

| Operation | Description                     | Example                                        |
| --------- | ------------------------------- | ---------------------------------------------- |
| forEach   | Perform action for each element | `list.stream().forEach(System.out::println)`   |
| collect   | Collect into List/Set/Map       | `list.stream().collect(Collectors.toList())`   |
| reduce    | Reduce to single value          | `list.stream().reduce(0, Integer::sum)`        |
| count     | Count elements                  | `list.stream().count()`                        |
| min       | Find min by comparator          | `list.stream().min(Comparator.naturalOrder())` |
| max       | Find max by comparator          | `list.stream().max(Comparator.naturalOrder())` |
| anyMatch  | Check if any element matches    | `list.stream().anyMatch(x -> x > 10)`          |
| allMatch  | Check if all match              | `list.stream().allMatch(x -> x > 0)`           |
| noneMatch | Check if none match             | `list.stream().noneMatch(String::isEmpty)`     |
| findFirst | Return first element            | `list.stream().findFirst()`                    |
| findAny   | Return any element              | `list.stream().findAny()`                      |

---

## 7. Handy Examples

### Example 1: Filter and Collect

```java
List<String> names = Arrays.asList("Alice", "Bob", "Ankit", "David");
List<String> result = names.stream()
                           .filter(n -> n.startsWith("A"))
                           .map(String::toUpperCase)
                           .collect(Collectors.toList());
System.out.println(result); // [ALICE, ANKIT]
```

### Example 2: Find Sum Using Reduce

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
int sum = numbers.stream().reduce(0, Integer::sum);
System.out.println(sum); // 15
```

### Example 3: Parallel Stream

```java
List<Integer> numbers = IntStream.range(1, 100).boxed().collect(Collectors.toList());
int total = numbers.parallelStream().reduce(0, Integer::sum);
System.out.println(total); // 4950
```

---

## 8. Alternatives to Streams

* **Traditional Loops (for/while/for-each)**: Good for indexed or simple operations.
* **Apache Commons / Guava**: Provide collection utilities (before Streams existed).
* **Iterators**: Explicit element traversal (but verbose).
* **Reactive Streams (RxJava, Project Reactor)**: For asynchronous, event-driven data flows.

---

## 9. Key Points

* Streams make code **declarative, concise, parallelizable**.
* Use **intermediate ops** to transform data lazily.
* Use **terminal ops** to produce results.
* Not always a replacement for loops; choose based on readability and performance.

---
