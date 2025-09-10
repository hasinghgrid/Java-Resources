# The Java Collections Framework: A Complete Guide

The **Java Collections Framework (JCF)** provides a unified architecture for storing and manipulating groups of objects. At its core are **interfaces** that define abstract data types, **implementations** which are concrete data structures, and **algorithms** that perform operations like searching and sorting.

---

## Java Collections Hierarchy Diagram

👉Collections-Hierarchy![Collections-Hierarchy](https://github.com/user-attachments/assets/07e0ed39-12bc-40e0-ae56-47afabd412e0)


Note that `Map` is part of the framework but does not extend the `Collection` interface.

---

## Core Collection Interfaces

The entire framework is built upon a few key interfaces.

### 1. Iterable Interface

* The **root interface** for the entire collection hierarchy.
* Its single method, `iterator()`, provides an `Iterator` to traverse the elements of the collection.
* Any class that implements `Iterable` can be used in the **for-each loop**.

### 2. Collection Interface

* The **foundation** of the framework.
* Declares the core methods that all collections will have, such as:

  * `add()`, `remove()`, `contains()`, `isEmpty()`, `size()`, `clear()`
* Represents a **group of objects**, known as its elements.

---

## List Interface

A **List** is an **ordered collection** (sometimes called a sequence) that allows **duplicate elements**. Users can access elements by their integer **index** and search for elements.

### Implementations of List

| Implementation | Underlying Structure         | Time Complexity (Average Case)                            | Best For                                  |
| -------------- | ---------------------------- | --------------------------------------------------------- | ----------------------------------------- |
| **ArrayList**  | Dynamic Array                | `get: O(1)`, `add: O(1)*`, `remove: O(n)`                 | Fast random access (by index)             |
| **LinkedList** | Doubly-Linked List           | `get: O(n)`, `add/remove: O(1)` at ends, `O(n)` in middle | Fast insertions/deletions, queues, deques |
| **Vector**     | Dynamic Array (Synchronized) | Same as ArrayList but with overhead                       | Thread-safe scenarios (legacy)            |

#### ArrayList

* **How it works**: Uses a dynamic array. When full, creates a larger array and copies elements.
* **Why**: Direct memory lookup → fast `get(i)` (O(1)).
* **When to use**: Default choice for a `List`. Ideal for frequent **index access**.
* 📚 *Example*: Library catalog where books are accessed by position.

#### LinkedList

* **How it works**: Stores elements in nodes linked by pointers.
* **Why**: Insertions/removals at ends are O(1), but `get(i)` is O(n).
* **When to use**: High number of **insertions/deletions**, especially at ends.
* 🎶 *Example*: Music playlist where songs are added/removed at ends.

#### Vector

* **How it works**: Same as `ArrayList`, but synchronized.
* **When to use**: In **legacy, thread-safe** scenarios.

---

## Set Interface

A **Set** is a collection that contains **no duplicate elements**.

### Implementations of Set

| Implementation    | Underlying Structure     | Order           | Time Complexity (Average Case) | Best For                          |
| ----------------- | ------------------------ | --------------- | ------------------------------ | --------------------------------- |
| **HashSet**       | Hash Table               | Unordered       | `add/remove/contains: O(1)`    | Fastest unique storage            |
| **LinkedHashSet** | Hash Table + Linked List | Insertion Order | `O(1)`                         | Unique + maintain insertion order |
| **TreeSet**       | Red-Black Tree           | Sorted Order    | `O(log n)`                     | Always sorted unique elements     |

#### HashSet

* **How it works**: Backed by `HashMap`. Elements stored as keys.
* **Why**: Hash table lookup = O(1).
* **When to use**: Store **unique items**, order not important.
* 🃏 *Example*: Deck of cards ensuring no duplicates.

#### TreeSet

* **How it works**: Backed by `TreeMap` (Red-Black Tree).
* **Why**: Keeps elements **sorted**.
* **When to use**: Unique elements, always sorted.
* 🏆 *Example*: Leaderboard with sorted scores.

---

## Queue Interface

A **Queue** is a collection used to hold elements prior to processing. Typically **FIFO (first-in, first-out)**.

### Implementations of Queue

| Implementation    | Underlying Structure | Order          | Time Complexity                      | Best For                   |
| ----------------- | -------------------- | -------------- | ------------------------------------ | -------------------------- |
| **LinkedList**    | Doubly-Linked List   | FIFO           | `O(1)`                               | General-purpose FIFO queue |
| **PriorityQueue** | Binary Heap          | Priority Order | `offer/poll: O(log n)`, `peek: O(1)` | Priority-based tasks       |
| **ArrayDeque**    | Dynamic Array        | FIFO/LIFO      | `O(1)`                               | Efficient queue or stack   |

#### PriorityQueue

* **How it works**: Binary heap, natural ordering or custom `Comparator`.
* **Why**: `offer/poll` reorganizes heap in O(log n).
* **When to use**: Processing items by **priority**.
* 🏥 *Example*: Emergency room patients prioritized by severity.

#### ArrayDeque

* **How it works**: Resizable array.
* **Why**: More efficient than `LinkedList`.
* **When to use**: Implementing queues/stacks.

---

## Deque Interface

A **Deque (double-ended queue)** supports insertion/removal at **both ends**.

* **ArrayDeque** is preferred (better locality of reference, all ops O(1)).
* **Use as**:

  * FIFO Queue
  * LIFO Stack

---

## Map Interface

A **Map** maps **keys to values**. No duplicate keys allowed. Not a true `Collection` but part of the framework.

### Implementations of Map

| Implementation    | Underlying Structure      | Key Order       | Time Complexity (Average Case) | Best For                    |
| ----------------- | ------------------------- | --------------- | ------------------------------ | --------------------------- |
| **HashMap**       | Hash Table                | Unordered       | `O(1)`                         | Fastest key-value storage   |
| **LinkedHashMap** | Hash Table + Linked List  | Insertion Order | `O(1)`                         | Predictable iteration order |
| **TreeMap**       | Red-Black Tree            | Sorted Order    | `O(log n)`                     | Sorted key-value pairs      |
| **Hashtable**     | Hash Table (Synchronized) | Unordered       | `O(1)`                         | Thread-safe legacy          |

#### HashMap

* **How it works**: Uses hashCode() to calculate bucket index.
* **Why**: `put/get` are O(1) on average.
* **When to use**: Default map implementation.
* 📞 *Example*: Phone book mapping names → numbers.

#### TreeMap

* **How it works**: Red-Black Tree keeps keys sorted.
* **Why**: Efficient O(log n) traversal.
* **When to use**: Always-sorted map.
* 📖 *Example*: Dictionary with words in alphabetical order.

#### Hashtable

* **How it works**: Like `HashMap` but synchronized.
* **When to use**: Legacy thread-safe scenarios. Prefer **ConcurrentHashMap** now.

---

# ✅ Summary

* **List** → Ordered, allows duplicates.
* **Set** → Unique, may be unordered/sorted.
* **Queue/Deque** → FIFO/LIFO ordering.
* **Map** → Key-value pairs, unique keys.
* **Choose implementation** based on ordering, performance, and thread-safety needs.

---
