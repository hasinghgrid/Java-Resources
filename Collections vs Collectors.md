# Collections vs Collectors in Java

Java provides two similar-sounding utility classes: **`Collections`** and **`Collectors`**.
They serve **different purposes** in the ecosystem of Java Collections and Streams.

---

## 📌 1. `Collections` (java.util.Collections)

* A **utility class** in `java.util`.
* Provides **static methods** to manipulate existing collections (`List`, `Set`, `Map`).
* Works with **traditional collections API** (not streams).

### Common Methods

* `Collections.sort(list)` → Sort a List
* `Collections.reverse(list)` → Reverse a List
* `Collections.shuffle(list)` → Random shuffle
* `Collections.binarySearch(list, key)` → Search in a sorted list
* `Collections.max(list)` → Find max element
* `Collections.min(list)` → Find min element
* `Collections.fill(list, value)` → Replace all elements with a value
* `Collections.copy(dest, src)` → Copy one list into another
* `Collections.swap(list, i, j)` → Swap elements
* `Collections.replaceAll(list, oldVal, newVal)` → Replace values
* `Collections.unmodifiableList(list)` → Read-only List
* `Collections.synchronizedList(list)` → Thread-safe List wrapper

### Example

```java
import java.util.*;

public class CollectionsExample {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>(Arrays.asList(4, 2, 9, 1, 5));

        Collections.sort(numbers);    // [1, 2, 4, 5, 9]
        Collections.reverse(numbers); // [9, 5, 4, 2, 1]

        Collections.swap(numbers, 0, 4); // swap first and last
        System.out.println("After swap: " + numbers);

        System.out.println("Max: " + Collections.max(numbers)); // 9
        System.out.println("Min: " + Collections.min(numbers)); // 1
    }
}
```

---

## 📌 2. `Collectors` (java.util.stream.Collectors)

* A **utility class** in `java.util.stream`.
* Provides **static factory methods** for collectors.
* Collectors are used with **Streams API** → `stream.collect(...)`.
* Helps gather stream results into **List, Set, Map, String, numbers, grouping, partitioning** etc.

### Common Collectors

* `Collectors.toList()` → Collect into a List
* `Collectors.toSet()` → Collect into a Set
* `Collectors.toMap(keyMapper, valueMapper)` → Collect into a Map
* `Collectors.joining(", ")` → Join into a String
* `Collectors.counting()` → Count elements
* `Collectors.summingInt(...)` / `summingLong(...)` / `summingDouble(...)` → Sum numbers
* `Collectors.averagingInt(...)` / `averagingDouble(...)` / `averagingLong(...)` → Average
* `Collectors.groupingBy(...)` → Group elements
* `Collectors.partitioningBy(predicate)` → Partition into two groups
* `Collectors.mapping(...)` → Apply mapping before collecting
* `Collectors.reducing(...)` → Custom reduction

### Example

```java
import java.util.*;
import java.util.stream.*;

public class CollectorsExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("John", "Jane", "Jack", "Jill", "Bob");

        // Collect into List
        List<String> upper = names.stream()
                .map(String::toUpperCase)
                .collect(Collectors.toList());
        System.out.println(upper); // [JOHN, JANE, JACK, JILL, BOB]

        // Count
        long count = names.stream().collect(Collectors.counting());
        System.out.println("Count: " + count); // 5

        // Join into a string
        String joined = names.stream().collect(Collectors.joining(", "));
        System.out.println("Joined: " + joined); // John, Jane, Jack, Jill, Bob

        // Group by length
        Map<Integer, List<String>> grouped = names.stream()
                .collect(Collectors.groupingBy(String::length));
        System.out.println(grouped); // e.g. {3=[Bob], 4=[John, Jane, Jack, Jill]}

        // Partitioning: names starting with J vs others
        Map<Boolean, List<String>> partitioned = names.stream()
                .collect(Collectors.partitioningBy(name -> name.startsWith("J")));
        System.out.println(partitioned); // {false=[Bob], true=[John, Jane, Jack, Jill]}
    }
}
```

---

## 🔑 Key Differences

| Feature    | **Collections** (java.util)     | **Collectors** (java.util.stream)      |
| ---------- | ------------------------------- | -------------------------------------- |
| Package    | `java.util`                     | `java.util.stream`                     |
| Type       | Utility class for collections   | Utility class for collectors (Streams) |
| Works with | `List`, `Set`, `Map`            | `Stream` API                           |
| Purpose    | Manipulate existing collections | Collect stream results                 |
| Example    | `Collections.sort(list)`        | `stream.collect(Collectors.toList())`  |

---

## ✅ Summary

* **Collections →** Works with traditional collections (sorting, searching, synchronization, etc.).
* **Collectors →** Works with streams to gather results into a collection, string, or aggregated form.
