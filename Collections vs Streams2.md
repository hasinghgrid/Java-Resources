# 📌 Collections vs Streams in Java

This document explains the **differences between Collections and Streams in Java**, when to use which, applications, and how they complement each other.

---

## 🔹 1. Basic Definition

### ✅ Collections
- A **Collection** is a **data structure** (e.g., `List`, `Set`, `Map`) that **stores elements in memory**.
- Represents a **container of objects**.
- Allows adding, removing, iterating, or modifying elements.

```java
List<String> names = new ArrayList<>();
names.add("Alice");
names.add("Bob");
```

### ✅ Streams
- A **Stream** is a **sequence of elements** derived from a collection, array, or I/O channel.
- **Not a data structure**; it doesn’t store elements.
- Provides an **abstraction for processing data** in a declarative, functional style.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.stream()
     .filter(n -> n.startsWith("A"))
     .forEach(System.out::println);
```

---

## 🔹 2. Key Differences

| Feature                  | **Collections**                                               | **Streams**                                                     |
|--------------------------|---------------------------------------------------------------|-----------------------------------------------------------------|
| **Nature**               | Data structure holding elements in memory.                   | Abstraction to process data (pipeline).                         |
| **Storage**              | Stores elements (can add/remove).                            | Doesn’t store elements, just processes them.                    |
| **Traversal**            | Can be traversed multiple times.                             | Usually traversed once (stream consumed after terminal op).     |
| **Modification**         | Supports add/remove/update.                                  | Cannot modify source; only transform/produce new results.       |
| **Execution**            | Eager (operations run immediately).                          | Lazy (runs only when a terminal operation is invoked).          |
| **Iteration**            | External iteration (`for`, `while`, `Iterator`).             | Internal iteration (handled by Stream API).                     |
| **Parallelism**          | Manual (threads, executors).                                 | Built-in support via `.parallelStream()`.                       |
| **Reusability**          | Reusable multiple times.                                     | One-time use (must recreate for reuse).                         |
| **API Style**            | Imperative (step-by-step).                                   | Declarative (what to do, not how).                              |

---

## 🔹 3. When to Use Collections

Use **Collections** when:
- You need to **store and manage data in memory**.
- You want to **add/remove/update elements** dynamically.
- You need **random access** (e.g., `list.get(5)`).

**Applications:**
- List of online users (`Set<User>`).
- Caching frequently used data.
- Implementing custom data structures (stack, queue, etc.).

---

## 🔹 4. When to Use Streams

Use **Streams** when:
- You need to **process or transform data**.
- You want **functional-style operations** like `map`, `filter`, `reduce`.
- You’re doing **bulk data operations** (aggregation, grouping, statistics).
- You need **parallel processing** easily.

**Examples:**

Filter orders:
```java
orders.stream()
      .filter(o -> o.getAmount() > 1000)
      .forEach(System.out::println);
```

Summing:
```java
int total = numbers.stream()
                   .mapToInt(Integer::intValue)
                   .sum();
```

Collecting:
```java
List<String> result = names.stream()
                           .map(String::toUpperCase)
                           .toList();
```

---

## 🔹 5. Complementary Usage

Most real-world Java apps **use both**:

```java
List<Employee> employees = getEmployees(); // Collection

// Stream for processing
double avgSalary = employees.stream()
                            .filter(e -> e.getDepartment().equals("IT"))
                            .mapToDouble(Employee::getSalary)
                            .average()
                            .orElse(0.0);
```

- **Collection** stores employees.
- **Stream** processes employees.

---

## 🔹 6. Which is Better?

It’s not about **better**, but about **purpose**:
- **Collections = Data storage & management.**
- **Streams = Data processing & transformation.**

👉 Use **Collections** for CRUD & storage.  
👉 Use **Streams** for transformations, filtering, aggregation.

---

⚡ **In practice:**
- Collections → Data layer.  
- Streams → Processing layer.
