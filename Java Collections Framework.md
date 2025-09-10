# The Java Collections Framework: A Complete Guide

The **Java Collections Framework (JCF)** provides a unified architecture for storing and manipulating groups of objects. At its core are:

* **Interfaces** → Abstract data types (List, Set, Queue, Map)
* **Implementations** → Concrete data structures (ArrayList, HashSet, HashMap, etc.)
* **Algorithms** → Utility methods (searching, sorting, shuffling, etc.)

---

## 📌 Java Collections Hierarchy Diagram

👉 Collections-Hierarchy 

![Collections-Hierarchy](https://github.com/user-attachments/assets/894d3933-90e9-4f29-9712-51653a7e1b64)

Note `Map` is not part of Collection framework

---

## 🔑 Core Collection Interfaces

The framework is built upon a few **key interfaces**.

### 1. **Iterable**

* **Root interface** of the entire hierarchy.
* Provides `iterator()` → used in enhanced **for-each loop**.

### 2. **Collection**

* **Foundation interface** for all collections.
* Declares core methods: `add()`, `remove()`, `contains()`, `isEmpty()`, `size()`, `clear()`.

---

## 📋 List Interface

An **ordered collection** (sequence) that allows **duplicates**.

| Implementation | Underlying Structure         | Time Complexity (Avg)                        | Best For                      |
| -------------- | ---------------------------- | -------------------------------------------- | ----------------------------- |
| **ArrayList**  | Dynamic Array                | get: O(1), add: O(1) amortized, remove: O(n) | Fast random access            |
| **LinkedList** | Doubly Linked List           | get: O(n), add/remove at ends: O(1)          | Frequent insertions/deletions |
| **Vector**     | Dynamic Array (Synchronized) | Similar to ArrayList, slower due to sync     | Legacy thread-safe list       |

✅ **When to use**:

* **ArrayList** → 📚 Library catalog (fast lookup by index)
* **LinkedList** → 🎶 Playlist (fast add/remove at ends)

---

## 🔢 Set Interface

A **collection with no duplicates**.

| Implementation    | Underlying Structure     | Order           | Time Complexity           | Best For                    |
| ----------------- | ------------------------ | --------------- | ------------------------- | --------------------------- |
| **HashSet**       | Hash Table (HashMap)     | Unordered       | add/remove/contains: O(1) | Fast lookup                 |
| **LinkedHashSet** | Hash Table + LinkedList  | Insertion Order | O(1)                      | Maintain order + uniqueness |
| **TreeSet**       | Red-Black Tree (TreeMap) | Sorted Order    | O(log n)                  | Always sorted               |

✅ **When to use**:

* **HashSet** → 🃏 Deck of cards (unique values)
* **TreeSet** → 🏆 Leaderboard (sorted unique scores)

---

## ⏩ Queue Interface

A **FIFO (First In, First Out)** data structure.

| Implementation    | Underlying Structure | Order          | Time Complexity                  | Best For              |
| ----------------- | -------------------- | -------------- | -------------------------------- | --------------------- |
| **LinkedList**    | Doubly Linked List   | FIFO           | O(1)                             | General-purpose queue |
| **PriorityQueue** | Binary Heap          | Priority Order | offer/poll: O(log n), peek: O(1) | Priority-based tasks  |
| **ArrayDeque**    | Resizable Array      | FIFO/LIFO      | O(1)                             | Efficient queue/stack |

✅ **When to use**:

* **PriorityQueue** → 🏥 ER patients (highest priority first)
* **ArrayDeque** → 📦 Undo/Redo stack or queue

---

## 🔄 Deque Interface

* **Double-ended queue** → insert/remove from both ends.
* **ArrayDeque** → preferred (faster than LinkedList).

✅ **Use cases** → Browser history, Undo/Redo.

---

## 🗺️ Map Interface

A **key-value pair** structure (not part of Collection).

| Implementation    | Underlying Structure      | Key Order       | Time Complexity | Best For                                   |
| ----------------- | ------------------------- | --------------- | --------------- | ------------------------------------------ |
| **HashMap**       | Hash Table                | Unordered       | O(1)            | General-purpose, fastest                   |
| **LinkedHashMap** | Hash Table + Linked List  | Insertion Order | O(1)            | Predictable iteration order                |
| **TreeMap**       | Red-Black Tree            | Sorted Order    | O(log n)        | Always sorted keys                         |
| **Hashtable**     | Hash Table (Synchronized) | Unordered       | O(1)            | Legacy thread-safe (use ConcurrentHashMap) |

✅ **When to use**:

* **HashMap** → 📞 Phonebook (fast key-value lookup)
* **TreeMap** → 📖 Dictionary (alphabetical order)

---

## 🚀 Summary Table

| Type      | Allows Duplicates? | Ordered?              | Key Feature       |
| --------- | ------------------ | --------------------- | ----------------- |
| **List**  | ✅ Yes              | ✅ Yes (Indexed)       | Random access     |
| **Set**   | ❌ No               | ❌/✅ (TreeSet)         | Uniqueness        |
| **Queue** | ✅ Yes              | ✅ FIFO/Priority       | Processing order  |
| **Deque** | ✅ Yes              | ✅ FIFO/LIFO           | Double-ended ops  |
| **Map**   | ❌ Keys unique      | Depends (Linked/Tree) | Key-value mapping |

---

✨ The Java Collections Framework provides **flexibility + performance**, allowing developers to choose the **right data structure** for each use case.
