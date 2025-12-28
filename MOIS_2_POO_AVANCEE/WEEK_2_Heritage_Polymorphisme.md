# MOIS_2_POO_AVANCEE/WEEK_2_Heritage_Polymorphisme.md : WEEK 2: Inheritance and Polymorphism

## Learning Objectives (3h)

| Objective | Why is it crucial? |
|---------|--------------------------|
| **Mastering Inheritance** | Avoid code duplication by creating specialized subclasses. |
| **Using `super()`** | Extend parent class functionalities without overwriting them completely. |
| **Understanding Polymorphism** | Use a unique interface for objects of different types. |
| **Composition vs Inheritance** | Knowing when to inherit and when to use an object inside another. |

---

## 1. Inheritance: Creating Hierarchies (1h)

Inheritance allows a class (child) to acquire attributes and methods from another (parent).

### Challenge 1: Secure Savings Account

**Objective:** Create a `SavingsAccount` with a strict withdrawal limit.

#### 📝 Guided Code: `super()`

```python
from bank_account import BankAccount

class SavingsAccount(BankAccount):
    def __init__(self, titular, balance, rate=0.05):
        super().__init__(titular, balance)  # Calls BankAccount's __init__
        self.rate = rate

    def withdraw(self, amount):
        if amount > 100000:
            print("❌ Withdrawal limit exceeded for a savings account.")
            return False
        return super().withdraw(amount)
```

> [!IMPORTANT]
> **Deep Dive: MRO (Method Resolution Order)**  
> In what order does Python look for a method? It uses the C3 Linearization algorithm. You can see this order by running `print(SavingsAccount.mro())`. This is vital for multiple inheritance.

---

## 2. Polymorphism: Flexibility (1h)

Polymorphism is the ability to perform the same action on different objects, each reacting in its own way.

### Challenge 2: Account Manager

```python
accounts = [BankAccount("John", 1000), SavingsAccount("Mary", 5000)]

for acc in accounts:
    acc.deposit(100) # Same call, but potentially different behavior
```

> [!TIP]
> **Pro Tip: Abstract Base Classes (ABCs)**  
> If you want to create a parent class that *cannot* be instantiated (a pure "blueprint"), use the `abc` module.  
> `from abc import ABC, abstractmethod`. This forces children to implement specific methods.

---

## 3. Composition vs Inheritance (30 min)

*   **Inheritance ("Is-a"):** A `Motorcycle` *is a* `Vehicle`.
*   **Composition ("Has-a"):** A `Car` *has an* `Engine`.

> [!WARNING]
> **Common Pitfall: Deep Inheritance**  
> Avoid creating hierarchies that are too deep (e.g., A -> B -> C -> D). This makes code rigid and fragile (the "Fragile Base Class problem"). Prefer composition if the relationship isn't a strong logical "is-a".

---

## 🧪 EXTRA EXERCISES (To go further)

### Exercise 1: OOP Zoo
Create an `Animal` class with a `speak()` method.
Create subclasses `Dog` and `Cat` that override `speak()`.
Create a function `make_animal_speak(animal)` that accepts any `Animal` (This is polymorphism!).

### Exercise 2: Notification System
Create a base `Notification` class.
Create `EmailNotification` and `SMSNotification`.
Implement a different `send()` method for each.
Simulate sending a mixed list of notifications.

---

## ⏳ Session Conclusion

  * **Review:** When to use `super()`? (To add behavior without deleting what already exists).
  * **Next Week:** We will learn to create methods bound to the class itself (Static and Class Methods).
