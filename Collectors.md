# 📌 Complete Guide to Collectors (`java.util.stream.Collectors`)

Collectors are one of the most useful parts of the Streams API. This guide covers **why they exist, how they work, the Collector interface anatomy, built-in collectors with examples, parallel collection behavior, custom collectors, and best practices**.

---

## 🔹 Why Collectors Exist & What They Solve

- Streams process sequences of elements, but usually you want a **result container** at the end (e.g., List, Map, String, aggregated value).
- **Collectors** provide a **reusable, composable way** to perform *mutable reduction*:
  - Accumulate elements into a mutable container.
  - Combine partial results (for parallel streams).
  - Transform the container into the final result.
- Compared to `reduce()`, collectors are:
  - More efficient for **mutable accumulation** (e.g., lists, maps).
  - Composable (downstream collectors for grouping, mapping, etc.).

---

## 🔹 Collector Interface Anatomy

```java
public interface Collector<T, A, R> {
  Supplier<A> supplier();                 // Create an empty result container
  BiConsumer<A, T> accumulator();         // Add an element to the container
  BinaryOperator<A> combiner();           // Merge two containers (parallel)
  Function<A, R> finisher();              // Convert container to final result
  Set<Characteristics> characteristics(); // Hints: CONCURRENT, UNORDERED, IDENTITY_FINISH
}
```

**Type Parameters:**
- `T` → Stream element type.
- `A` → Mutable accumulator type (intermediate container).
- `R` → Final result type.

➡️ `Collector.of(...)` is a factory for creating custom collectors.

---

## 🔹 How `collect()` Works (High-Level)

1. `supplier()` → creates empty accumulator.
2. Each element → `accumulator()` mutates the container.
3. If parallel → multiple accumulators created, merged with `combiner()`.
4. `finisher()` converts accumulator → final result.

- **Sequential:** one accumulator, one finisher.
- **Parallel:** multiple accumulators, merged, then finished.

---

## 🔹 Collector Characteristics

- **IDENTITY_FINISH** → `A == R`, no finishing step required.
- **UNORDERED** → Result does not depend on stream order.
- **CONCURRENT** → Accumulator is thread-safe, can be used across threads.

➡️ These characteristics help optimize concurrency and ordering.

---

## 🔹 Mutable vs Immutable Reduction

- **`reduce()`** → best for immutable reductions (summing, min/max).
- **`collect()`** → best for mutable reductions (lists, maps, sets).

---

## 🔹 Common Built-in Collectors with Examples

### 1. **toList()**
```java
List<String> list = stream.collect(Collectors.toList());
```
- Produces a `List` (usually `ArrayList`).
- Mutability not guaranteed (use `toUnmodifiableList()` for unmodifiable).

---

### 2. **toSet()**
```java
Set<String> set = stream.collect(Collectors.toSet());
```
- Produces a `Set` (usually `HashSet`).
- No order guarantee.

---

### 3. **toMap()**
```java
Map<Integer, String> map = stream.collect(Collectors.toMap(
    String::length, s -> s, (a, b) -> a + "," + b));
```
- Duplicate keys throw `IllegalStateException` unless merge function provided.
- Overloads allow custom map supplier.

---

### 4. **joining()**
```java
String csv = stream.collect(Collectors.joining(", "));
String withBrackets = stream.collect(Collectors.joining(", ", "[", "]"));
```
- Concatenates CharSequences efficiently using `StringBuilder`.

---

### 5. **counting()**
```java
Long count = stream.collect(Collectors.counting());
```
- Returns boxed `Long`.
- Equivalent to `stream.count()` but fits into collector pipelines.

---

### 6. **summingInt / summingLong / summingDouble**
```java
Integer total = stream.collect(Collectors.summingInt(String::length));
```
- Returns boxed primitive wrapper type.

---

### 7. **averagingInt / averagingDouble**
```java
Double avg = stream.collect(Collectors.averagingInt(String::length));
```
- Always returns `Double`.

---

### 8. **maxBy / minBy**
```java
Optional<String> max = stream.collect(Collectors.maxBy(Comparator.naturalOrder()));
```
- Returns `Optional<T>`.

---

### 9. **groupingBy**
```java
Map<Integer, List<String>> grouped =
    stream.collect(Collectors.groupingBy(String::length));

Map<Integer, Set<String>> groupedSet =
    stream.collect(Collectors.groupingBy(String::length, Collectors.toSet()));
```
- Extremely powerful with downstream collectors.
- `groupingByConcurrent()` for concurrent grouping.

---

### 10. **partitioningBy**
```java
Map<Boolean, List<Integer>> parts =
    nums.stream().collect(Collectors.partitioningBy(n -> n % 2 == 0));
```
- Specialized case of grouping → partitions into `true/false` buckets.

---

### 11. **mapping**
```java
Set<Integer> lengths = stream.collect(
    Collectors.mapping(String::length, Collectors.toSet()));
```
- Transforms before downstream collector.

---

### 12. **reducing**
```java
Optional<Integer> sum = stream.collect(Collectors.reducing(Integer::sum));
Integer sum2 = stream.collect(Collectors.reducing(0, String::length, Integer::sum));
```
- General-purpose reduction inside collector framework.

---

### 13. **collectingAndThen**
```java
List<String> immutable = stream.collect(
    Collectors.collectingAndThen(Collectors.toList(), Collections::unmodifiableList));
```
- Post-process collector result (e.g., wrap in unmodifiable list).

---

## 🔹 Examples (Compact)

```java
List<String> strings = List.of("a", "bb", "ccc");

// toList
List<String> list = strings.stream().collect(Collectors.toList());

// toMap with merge
Map<Integer, String> map = strings.stream()
    .collect(Collectors.toMap(String::length, s -> s, (a, b) -> a + "|" + b));

// groupingBy with mapping
Map<Integer, Set<String>> grouped = strings.stream()
    .collect(Collectors.groupingBy(String::length,
             Collectors.mapping(Function.identity(), Collectors.toSet())));

// counting
Long count = strings.stream().collect(Collectors.counting());

// joining
String joined = strings.stream().collect(Collectors.joining(", "));
```

---

## 🔹 Parallel Streams & Collectors (Simplified Internals)

- **Sequential:** one accumulator → accumulate → finisher.
- **Parallel:**
  - Stream splits into chunks.
  - Each subtask has its own accumulator.
  - Partial accumulators merged with combiner.
  - Finisher applied to result.
- **Concurrent collectors** (e.g., `groupingByConcurrent`) may accumulate into one shared container.

---

## 🔹 Writing Your Own Collector

Example: Join strings with commas.

```java
Collector<String, StringBuilder, String> joiner = Collector.of(
    StringBuilder::new,
    (sb, s) -> { if (sb.length() > 0) sb.append(","); sb.append(s); },
    (sb1, sb2) -> { if (sb1.length() > 0 && sb2.length() > 0) sb1.append(","); sb1.append(sb2); return sb1; },
    StringBuilder::toString
);

String result = Stream.of("a", "b", "c").collect(joiner);
```

---

## 🔹 Downstream Collectors & Composition

- `groupingBy(classifier, downstream)` → e.g., `groupingBy(fn, counting())`.
- `mapping(mapper, downstream)` → transform before collecting.
- `collectingAndThen(downstream, finisher)` → apply final transformation.

```java
Map<Integer, Long> sizeCounts = stream.collect(
    Collectors.groupingBy(String::length, Collectors.counting()));
```

---

## 🔹 Performance Tips & Best Practices

- For parallel → use `groupingByConcurrent` / `toConcurrentMap`.
- Prefer **built-in collectors** (highly optimized).
- For predictable sizes, use `toCollection(() -> new ArrayList<>(expectedSize))`.
- Use `toUnmodifiableList()` (Java 10+) for immutability.
- Avoid shared mutable state unless using concurrent collectors.

---

## 🔹 Common Pitfalls

- `toMap()` → throws on duplicates unless merge function provided.
- Not all collectors are thread-safe.
- Ordering may or may not be preserved.
- Misusing `CONCURRENT` → ensure thread-safe accumulator.

---

## 🔹 Quick Cheat-Sheet

| Collector           | Returns                  | Example |
|---------------------|--------------------------|---------|
| **toList()**        | `List<T>`                | `stream.collect(toList())` |
| **toSet()**         | `Set<T>`                 | `stream.collect(toSet())` |
| **toMap()**         | `Map<K,V>`               | `toMap(String::length, s->s, (a,b)->a+","+b)` |
| **joining()**       | `String`                 | `Collectors.joining(", ")` |
| **counting()**      | `Long`                   | `Collectors.counting()` |
| **summingInt()**    | `Integer`                | `summingInt(String::length)` |
| **averagingInt()**  | `Double`                 | `averagingInt(...)` |
| **maxBy/minBy**     | `Optional<T>`            | `maxBy(Comparator.naturalOrder())` |
| **groupingBy**      | `Map<K, List<T>>`        | `groupingBy(String::length)` |
| **partitioningBy**  | `Map<Boolean, List<T>>`  | `partitioningBy(predicate)` |
| **mapping**         | Transform + downstream   | `mapping(String::length, toSet())` |
| **reducing**        | Custom reduction         | `reducing(0, String::length, Integer::sum)` |
| **collectingAndThen** | Post-process result    | `collectingAndThen(toList(), unmodifiableList())` |

---

## 🔹 When to Use Which

- **Build collections** → `toList`, `toSet`, `toMap`.
- **Grouping** → `groupingBy`, with downstreams.
- **Partitioning** → `partitioningBy`.
- **Statistics** → `counting`, `summingInt`, `averagingInt`, `maxBy`.
- **String building** → `joining`.
- **Post-process** → `collectingAndThen`.
- **Parallel performance** → `groupingByConcurrent`, `toConcurrentMap`.
