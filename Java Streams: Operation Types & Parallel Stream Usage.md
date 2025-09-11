# Java Streams: Operation Types & Parallel Stream Usage

## 1. Types of Stream Operations

### A. Intermediate Operations

* **Definition:** Transform a stream into another stream.
* **Execution:** Lazy (only when a terminal operation is invoked).
* **Examples:** `filter`, `map`, `flatMap`, `sorted`, `distinct`, `limit`, `skip`
* ✅ Use when you need to transform/filter before final processing.
* ❌ Avoid chaining too many trivial ones for readability.

---

### B. Terminal Operations

* **Definition:** End the stream pipeline and produce a result or side-effect.
* **Execution:** Immediate.
* **Examples:** `forEach`, `collect`, `reduce`, `count`, `min`, `max`
* ✅ Use for producing results.
* ❌ Avoid `forEach` for data collection → prefer `collect`.

---

### C. Stateless Operations

* **Definition:** Each element is processed independently.
* **Examples:** `map`, `filter`, `flatMap`, `peek`
* ✅ Works well with parallel streams.
* ❌ Avoid when logic depends on element order.

---

### D. Stateful Operations

* **Definition:** Require knowledge of other elements.
* **Examples:** `distinct`, `sorted`, `limit`, `skip`
* ⚠️ May cause memory overhead.
* ❌ Avoid for very large datasets if performance is critical.

---

### E. Short-circuit Operations

* **Definition:** May terminate without processing all elements.
* **Examples:** `findFirst`, `findAny`, `anyMatch`, `allMatch`, `noneMatch`, `limit`
* ✅ Efficient when partial results are sufficient.
* ❌ Useless if all elements must be processed.

---

## 2. Parallel Streams: When to Use & When Not To

### ✅ When to Use Parallel Streams

* **CPU-bound, independent tasks** (e.g., heavy computation).
* **Large datasets** (10k+ elements).
* **Stateless operations** like `map`, `filter`.
* **Unordered operations** (`forEach`, `findAny`).
* **Multi-core environments**.

**Example:**

```java
long count = list.parallelStream()
                 .filter(this::isPrime)
                 .count();
```

---

### ❌ When Not to Use Parallel Streams

* **Small datasets** (overhead > benefit).
* **I/O-bound tasks** (DB, network) → use async/reactive.
* **Order-sensitive ops** (`forEachOrdered`, non-associative `reduce`).
* **Stateful lambdas** (modifying shared state → race conditions).
* **Collectors without CONCURRENT support** (`Collectors.toMap()` can fail).
* **ForkJoinPool contention** (streams share the common pool).

---

## 3. Rule of Thumb

* Start with **sequential streams**.
* Use **parallel streams** only when:

  * Task is **CPU-heavy**
  * Dataset is **large**
  * Operations are **independent & stateless**
  * Performance profiling shows **clear benefit**

---

## 4. Quick Comparison Table

| Aspect               | Sequential Stream | Parallel Stream              |
| -------------------- | ----------------- | ---------------------------- |
| Execution Model      | Single-threaded   | Multi-threaded               |
| Best for             | Small/medium data | Large, CPU-bound data        |
| Memory Overhead      | Low               | Higher (splitting & merging) |
| Order Preservation   | Guaranteed        | Not always (unless forced)   |
| Shared Mutable State | Safe              | Risk of race conditions      |
| I/O-bound Work       | No advantage      | No advantage                 |
