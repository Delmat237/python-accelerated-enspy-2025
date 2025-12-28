# MOIS_2_POO_AVANCEE/WEEK_1_Classes_Encapsulation.md : WEEK 1: Classes and Encapsulation

### **Complete Course – Theoretical Explanations Before Code**

---

## Learning Objectives (3h – Explanatory Approach)

| Objective | Why is it crucial? |
|---------|--------------------------|
| **Understanding OOP** | Model the real world (bank, hospital, agriculture). |
| **Mastering `class` and `__init__`** | Create reusable and consistent objects. |
| **Applying Encapsulation** | Protect critical data (e.g., bank balance). |
| **Using `@property`** | Control access without breaking the public interface. |
| **Real Lab** | Build a **complete banking system**. |

---

## 1. Introduction to OOP: Why? (30 min – Theory)

> **"Everything is an object in Python."**  
> If you run `type(5)` or `type("hello")`, Python returns `<class 'int'>` or `<class 'str'>`. OOP isn't just an option; it's the core of Python.

### Real Problem: Bank Account Management

An account has data (balance, titular) and behaviors (deposit, withdraw).  
Without OOP, data is scattered. With OOP, it's unified into a single entity: **The Object**.

---

## 2. Class Fundamentals (45 min – Theory + Example)

### What is a **Class**?

It's the **blueprint**. An **Object** (or instance) is the house built from that blueprint.

| Concept | Analogy | Code |
|--------|---------|--------|
| **Class** | Car blueprint | `class Car:` |
| **Object** | A specific Toyota | `my_car = Car()` |
| **Attribute** | State (Color, Speed) | `self.color = "Red"` |
| **Method** | Action (Drive, Brake) | `def drive(self):` |

---

### `self`: The link to the instance

`self` represents the specific object calling the method. Without it, Python wouldn't know which balance to modify if you have 1000 accounts open.

> [!IMPORTANT]
> **Deep Dive: The `__init__` Constructor**  
> It's not strictly "the creator" of the object (that's `__new__`), but it's the **initializer**. It prepares the object right after birth by giving it starting values.

---

## 3. Encapsulation: Protecting Data (45 min – Theory)

### The Concept of "Professional Secrecy"

In OOP, we don't want users touching the internal guts of an object. We use conventions:

| Prefix | Meaning | Python's Behavior |
|--------|-----------|--------|
| `name` | **Public** | Accessible from anywhere. |
| `_name` | **Protected** | *Convention*: "Please don't touch this from the outside." |
| `__name` | **Private** | **Name Mangling**: Python changes the internal name (e.g., `_Account__name`) to make accidental access very difficult. |

---

### `@property`: The Power of Getters/Setters

Instead of writing `get_balance()` and `set_balance()`, Python offers an elegant syntax:

```python
class Account:
    def __init__(self):
        self._balance = 0

    @property
    def balance(self):
        return f"{self._balance} FCFA"

    @balance.setter
    def balance(self, value):
        if value < 0:
            raise ValueError("Negative balance forbidden!")
        self._balance = value
```

> [!TIP]
> **Pro Tip: Uniform Interface**  
> Thanks to `@property`, you can turn a simple attribute into a calculated method later, without making users change their code from `obj.balance` to `obj.get_balance()`. This is key for long-term maintenance.

---

## 4. Integration Lab: Banking System (45 min)

### `bank_account.py` (Enriched Snippet)

```python
class BankAccount:
    def __init__(self, titular: str, initial_balance: float = 0.0):
        self.titular = titular
        self._balance = initial_balance
        self.__bank_secret = "Code-123" # Private (Name mangling)

    def deposit(self, amount: float):
        if amount <= 0:
            raise ValueError("Positive amount required")
        self._balance += amount
        print(f"New balance: {self.balance}")

    @property
    def balance(self):
        return self._balance
```

> [!WARNING]
> **Common Pitfall: Circular Imports**  
> If class `Bank` needs `Account` and `Account` needs `Bank`, your program will crash.  
> *Solution:* Import only what is necessary inside methods, or use type-hinting strings like `"Bank"`.

---

## 🧪 EXTRA EXERCISES (To go further)

### Exercise 1: OOP Stock Manager
Create a `Product` class with `name`, `price`, and `quantity`.
Use a `@property` for `price` that prevents setting a price below 100 FCFA.
Add a `sell(n)` method that decreases quantity and shows an error if stock is insufficient.

### Exercise 2: Circle and Radius
Create a `Circle` class.
The attribute is `radius`.
Add properties for `diameter` and `area` (calculated on the fly).
If the `diameter` is changed via a setter, the `radius` must update automatically!

---

## ⏳ Conclusion & Week 2 Preparation

  * **Review:** What is the difference between `_var` and `__var`?
  * **Next Week:** We will see how to create families of classes (Inheritance) and how a single command can have multiple effects (Polymorphism).
