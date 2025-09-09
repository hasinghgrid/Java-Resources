# 🧠 Comparator vs Comparable in Java

---

## 🔹 Feature Comparison

| Feature              | Comparable                          | Comparator                                   |
|----------------------|-------------------------------------|---------------------------------------------|
| **Package**          | `java.lang`                        | `java.util`                                 |
| **Interface method** | `compareTo(T o)`                   | `compare(T o1, T o2)`                       |
| **Use case**         | Natural/default ordering            | Custom, multiple sorting logics             |
| **Modified class?**  | ✅ Yes (class must implement)       | ❌ No (can define externally, flexible)     |
| **Example**          | `String`, `Integer` (natural sort) | Sorting by age, salary, name, etc.          |

---

## 🔹 Code Examples

### Comparable Example
```java
class Student implements Comparable<Student> {
    int marks;
    String name;

    @Override
    public int compareTo(Student other) {
        return Integer.compare(this.marks, other.marks); // natural ordering by marks
    }
}
```

### Comparator Example
```java
Comparator<Student> byName = Comparator.comparing(student -> student.name);
Comparator<Student> byMarks = Comparator.comparingInt(student -> student.marks);

students.sort(Comparator.comparingInt((Student s) -> s.marks)
                        .thenComparing(s -> s.name));
```

---

## 🔹 `==`, `.equals()`, and `hashCode()`
- `==` → compares references (memory location).
- `.equals()` → compares logical equality (content).
- `hashCode()` → ensures objects that are equal have the same hash for hash-based collections.

---

# ✅ Insertion-Order-Preserving Data Structures in Java

### 1. `LinkedHashMap<K, V>`
- Maintains insertion order of keys.
- Inherits from `HashMap`.

```java
Map<String, Integer> map = new LinkedHashMap<>();
map.put("A", 1);
map.put("B", 2);
map.put("C", 3);
System.out.println(map); // {A=1, B=2, C=3}
```

### 2. `LinkedHashSet<E>`
- Maintains insertion order of unique elements.

```java
Set<String> set = new LinkedHashSet<>();
set.add("Apple");
set.add("Banana");
set.add("Cherry");
System.out.println(set); // [Apple, Banana, Cherry]
```

### 3. `ArrayList<E>`
- Maintains insertion order of elements.
- Allows duplicates and `null`.

```java
List<String> list = new ArrayList<>();
list.add("X");
list.add("Y");
list.add("Z");
System.out.println(list); // [X, Y, Z]
```

### ❌ Not Insertion Ordered
- `HashMap`, `HashSet` → no guaranteed order.
- `TreeMap`, `TreeSet` → sorted by keys/elements (not insertion).

### 🔍 Summary Table
| Data Structure | Maintains Insertion Order? | Allows Duplicates? |
|----------------|-----------------------------|---------------------|
| LinkedHashMap  | ✅ Yes                      | Keys: ❌, Values: ✅ |
| LinkedHashSet  | ✅ Yes                      | ❌ No               |
| ArrayList      | ✅ Yes                      | ✅ Yes              |
| HashMap        | ❌ No                       | Keys: ❌, Values: ✅ |
| TreeMap        | ❌ (Sorted by keys)         | ✅ Yes              |

---

# 🔒 Concurrent Collections

| Collection             | Use When                                      |
|-------------------------|-----------------------------------------------|
| `ConcurrentHashMap`     | High-speed concurrent read/write map          |
| `CopyOnWriteArrayList`  | Many reads, few writes                        |
| `BlockingQueue`         | Thread coordination (producer/consumer)       |
| `ConcurrentSkipListMap` | Concurrent sorted map                         |
| `ConcurrentLinkedQueue` | Lock-free, FIFO queue                         |

---

# 🧩 Thread Lifecycle

1. **New** → created but not started.
2. **Runnable** → eligible to run.
3. **Running** → executing.
4. **Blocked / Waiting / Sleeping** → paused.
5. **Terminated (Dead)** → finished execution.

---

# 🛠️ How to Create Threads

### 1. Extend `Thread`
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}
new MyThread().start();
```

### 2. Implement `Runnable`
```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable thread: " + Thread.currentThread().getName());
    }
}
new Thread(new MyRunnable()).start();
```

### 3. Use Lambda (Java 8+)
```java
new Thread(() -> System.out.println("Lambda Thread")).start();
```

---

# ✅ Runnable vs Thread (Extending)

| Feature           | `implements Runnable`             | `extends Thread`                    |
|-------------------|-----------------------------------|-------------------------------------|
| **Inheritance**   | Allows extending another class    | Can’t extend any other class        |
| **Reusability**   | Better separation of concern      | Less reusable                       |
| **Flexibility**   | Works with thread pools           | Less flexible                       |
| **Best for**      | Sharing tasks across threads      | Quick one-off threading             |
| **Real-world use**| ✅ Yes (with ExecutorService)     | ❌ Rarely used                       |

👉 **Always prefer Runnable** in real-world apps for flexibility & thread pooling.

---

# 🔢 Autoboxing & Unboxing in Collections

- Java Collections work only with **objects**, not primitives.

```java
List<Integer> list = new ArrayList<>();
list.add(10); // autoboxing: int → Integer
int value = list.get(0); // unboxing: Integer → int
```

Without autoboxing:
```java
list.add(Integer.valueOf(10));
int value = list.get(0).intValue();
