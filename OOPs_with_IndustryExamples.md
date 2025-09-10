# 🚀 4 Pillars of OOP with Real-Life Software Examples

## 1️⃣ Abstraction

**Definition**: Hiding implementation details and exposing only essential features.

**Real-Life Example (Banking Software)**

* In net banking apps, customers see simple actions like *transferMoney()* or *checkBalance()*.
* They don’t see how transactions are verified, how databases are queried, or how ledgers are updated.

```java
abstract class BankTransaction {
    abstract void processTransaction(double amount);
}

class UpiTransaction extends BankTransaction {
    @Override
    void processTransaction(double amount) {
        System.out.println("Processing UPI transaction of Rs." + amount);
    }
}

class CardTransaction extends BankTransaction {
    @Override
    void processTransaction(double amount) {
        System.out.println("Processing Card transaction of Rs." + amount);
    }
}
```

✅ User interacts only with `processTransaction()` without knowing the complex internals.

---

## 2️⃣ Encapsulation

**Definition**: Wrapping data (fields) and methods together in a class, restricting direct access.

**Real-Life Example (Healthcare / EMR Systems)**

* Patient medical records are sensitive and private.
* Only authorized methods can access/update them — not directly accessible.

```java
class PatientRecord {
    private String name;
    private String medicalHistory;

    public PatientRecord(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void updateMedicalHistory(String history, boolean isDoctor) {
        if(isDoctor) {
            this.medicalHistory = history;
        } else {
            System.out.println("Access denied! Only doctors can update records.");
        }
    }
}
```

✅ Prevents unauthorized modification of sensitive data.

---

## 3️⃣ Inheritance

**Definition**: Creating new classes from existing ones, enabling code reuse.

**Real-Life Example (Ride-Sharing Apps - Uber/Ola)**

* Different vehicle types (Car, Bike, Auto) inherit from a common `Vehicle` base class.

```java
class Vehicle {
    String registrationNumber;
    void startRide() {
        System.out.println("Ride started...");
    }
}

class Car extends Vehicle {
    int seats = 4;
}

class Bike extends Vehicle {
    boolean helmetProvided = true;
}
```

✅ Common features are reused across multiple vehicle types, reducing duplication.

---

## 4️⃣ Polymorphism

**Definition**: Ability of an object to take many forms (method overriding/overloading).

**Real-Life Example (E-commerce Payment Gateway)**

* Payment processing works with different payment modes (Credit Card, UPI, PayPal).

```java
class PaymentService {
    void pay(double amount) {
        System.out.println("Generic payment of Rs." + amount);
    }
}

class UpiPayment extends PaymentService {
    @Override
    void pay(double amount) {
        System.out.println("Paid Rs." + amount + " via UPI");
    }
}

class CardPayment extends PaymentService {
    @Override
    void pay(double amount) {
        System.out.println("Paid Rs." + amount + " via Card");
    }
}
```

✅ Same method `pay()` behaves differently depending on payment mode.

---

# 🔍 Summary Table

| OOP Pillar        | Real-World Software Example          | Benefit                 |
| ----------------- | ------------------------------------ | ----------------------- |
| **Abstraction**   | Banking Apps (Transactions)          | Hides complexity        |
| **Encapsulation** | Healthcare Systems (Patient Records) | Secure data             |
| **Inheritance**   | Ride-Sharing Apps (Vehicles)         | Code reuse              |
| **Polymorphism**  | E-commerce Payments                  | Flexibility in behavior |

---
