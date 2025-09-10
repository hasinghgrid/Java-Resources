# Comparators in Java

Comparators are a core part of Java's **sorting and ordering mechanisms**. They allow developers to define **custom rules** for comparing objects, which is especially useful when objects don't have a natural order or when you want to sort them differently than their natural order.

---

## 📌 Why Comparators?

* **Default ordering (Comparable):** Java classes can implement the `Comparable` interface to define a natural ordering (`compareTo` method). Example: `String` and `Integer` implement Comparable.
* **Custom ordering (Comparator):** When you need multiple or custom sorting strategies without changing the class itself, you use `Comparator`.
* **Flexibility:** Comparators let you plug in different sorting logic at runtime.

### Example: Comparable vs Comparator

```java
class Person implements Comparable<Person> {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() { return name; }
    public int getAge() { return age; }

    // Natural order: by name
    @Override
    public int compareTo(Person other) {
        return this.name.compareTo(other.name);
    }
}

// Comparator usage: sort by age instead of name
Comparator<Person> byAge = Comparator.comparingInt(Person::getAge);
```

---

## 📌 Common Comparator Methods

| Method                     | Description                                        | Example                                                                            |
| -------------------------- | -------------------------------------------------- | ---------------------------------------------------------------------------------- |
| **`naturalOrder()`**       | Sort in ascending order (natural order).           | `list.stream().sorted(Comparator.naturalOrder())`                                  |
| **`reverseOrder()`**       | Sort in descending order (natural order reversed). | `list.stream().sorted(Comparator.reverseOrder())`                                  |
| **`comparing(...)`**       | Compare objects by a property.                     | `list.stream().sorted(Comparator.comparing(String::length))`                       |
| **`comparingInt(...)`**    | Compare by an `int` property.                      | `list.stream().sorted(Comparator.comparingInt(String::length))`                    |
| **`comparingLong(...)`**   | Compare by a `long` property.                      | `list.stream().sorted(Comparator.comparingLong(Person::getAge))`                   |
| **`comparingDouble(...)`** | Compare by a `double` property.                    | `list.stream().sorted(Comparator.comparingDouble(Product::getPrice))`              |
| **`thenComparing(...)`**   | Tie-breaker comparator.                            | `Comparator.comparingInt(String::length).thenComparing(Comparator.naturalOrder())` |
| **`reversed()`**           | Reverse the comparator.                            | `Comparator.comparingInt(String::length).reversed()`                               |
| **`nullsFirst(...)`**      | Null values appear before non-null values.         | `Comparator.nullsFirst(Comparator.naturalOrder())`                                 |
| **`nullsLast(...)`**       | Null values appear after non-null values.          | `Comparator.nullsLast(Comparator.naturalOrder())`                                  |

---

## 📌 Detailed Examples

### 1. Natural Order vs Reverse Order

```java
List<Integer> numbers = Arrays.asList(5, 2, 8, 1);

// Ascending
numbers.stream()
       .sorted(Comparator.naturalOrder())
       .forEach(System.out::println); // 1, 2, 5, 8

// Descending
numbers.stream()
       .sorted(Comparator.reverseOrder())
       .forEach(System.out::println); // 8, 5, 2, 1
```

### 2. Comparing by Property

```java
List<String> words = Arrays.asList("apple", "pear", "banana");

words.stream()
     .sorted(Comparator.comparing(String::length))
     .forEach(System.out::println); // pear, apple, banana
```

### 3. Multiple Comparisons (thenComparing)

```java
List<Person> people = Arrays.asList(
    new Person("Alice", 30),
    new Person("Bob", 25),
    new Person("Charlie", 25)
);

// First by age, then by name
people.stream()
      .sorted(Comparator.comparingInt(Person::getAge)
      .thenComparing(Person::getName))
      .forEach(p -> System.out.println(p.getName()));
```

### 4. Handling Nulls

```java
List<String> items = Arrays.asList("apple", null, "banana");

// Nulls first
items.stream()
     .sorted(Comparator.nullsFirst(Comparator.naturalOrder()))
     .forEach(System.out::println); // null, apple, banana

// Nulls last
items.stream()
     .sorted(Comparator.nullsLast(Comparator.naturalOrder()))
     .forEach(System.out::println); // apple, banana, null
```

---

## 📌 When to Use Comparator

* When a class **does not implement Comparable**.
* When you want **multiple sorting strategies** for the same class.
* When sorting rules must be **decoupled from the class definition**.
* When handling **null values safely** in sorting.
* When sorting by **derived/calculated properties**.

---

## ✅ Summary

* **Comparable** → Defines natural order inside the class (`compareTo`).
* **Comparator** → Defines custom order outside the class (flexible, multiple strategies).
* **Comparator methods** like `comparing`, `thenComparing`, `reversed`, `nullsFirst`, and `nullsLast` make sorting powerful and concise.

```java
// Example summary: sort people by age descending, then by name ascending
people.sort(Comparator.comparingInt(Person::getAge)
                      .reversed()
                      .thenComparing(Person::getName));
```

Comparators give **fine-grained control** over ordering, essential for collections and stream operations.
