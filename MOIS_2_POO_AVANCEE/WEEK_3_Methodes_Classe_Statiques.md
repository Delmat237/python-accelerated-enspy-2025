# MOIS_2_POO_AVANCEE/WEEK_3_Methodes_Classe_Statiques.md : WEEK 3: Class and Static Methods

## Learning Objectives (3h)

| Objective | Why is it crucial? |
|---------|--------------------------|
| **Understanding `@classmethod`** | Handle data related to the class itself. |
| **Using `@staticmethod`** | Create logically grouped utility functions. |
| **The Factory Pattern** | Learn to create objects in various elegant ways. |
| **Managing Class Attributes** | Share information across all instances securely. |

---

## 1. Class Methods: Shared Information (1h)

A class method receives the class itself (`cls`) as its first argument.

### Challenge 1: Global Account Counter

**Objective:** Track the total number of accounts created across the entire bank.

#### 📝 Guided Code: `@classmethod`

```python
class Bank:
    total_accounts_count = 0 # Class attribute

    def __init__(self, titular):
        self.titular = titular
        Bank._increment_counter()

    @classmethod
    def _increment_counter(cls):
        cls.total_accounts_count += 1

    @classmethod
    def display_stats(cls):
        print(f"The bank manages {cls.total_accounts_count} accounts in total.")
```

> [!TIP]
> **Pro Tip: The "Factory" Pattern**  
> Class methods are perfect for creating objects with different data sources.  
> `Account.from_json(raw_data)` or `Date.today()`. This allows you to have multiple named "constructors".

---

## 2. Static Methods: Utilities (1h)

A static method is a function that needs neither `self` nor `cls`, but logically belongs to the class.

### Challenge 2: Currency Validator

#### 📝 Guided Code: `@staticmethod`

```python
class FinanceUtils:
    @staticmethod
    def is_currency_valid(currency):
        return currency.upper() in ["FCFA", "EUR", "USD"]
```

> [!IMPORTANT]
> **Deep Dive: Method Comparison**
>
> | Type | Decorator | First Arg | Access |
| :--- | :--- | :--- | :--- |
| **Instance** | None | `self` | Object attributes |
| **Class** | `@classmethod` | `cls` | Class attributes |
| **Static** | `@staticmethod` | None | None (independent) |

---

## 3. When to Use What? (30 min)

> [!WARNING]
> **Common Pitfall: Overusing `@staticmethod`**  
> If your static method has no logical link to the class, it's better to make it a simple function at the top of your file. `@staticmethod` should only be used to group utilities that make sense *within* the context of the class.

---

## 🧪 EXTRA EXERCISES (To go further)

### Exercise 1: Temperature Converter
Create a `Temperature` class.
Add a class method `from_fahrenheit(value)` that returns an instance of `Temperature` converted to Celsius.
Add a static method `is_cold(celsius)` that returns `True` if temp is < 10.

### Exercise 2: User Manager
Create a `User` class.
Add a class attribute `active_users` (a list).
Every time a user is created, add them to the list via a class method.
Add a class method `find_user(name)` that searches the global list.

---

## ⏳ Session Conclusion

  * **Review:** Why use `cls` instead of hardcoding the class name? (So that inheritance works correctly!).
  * **Next Week:** We will add the finishing touch: Unit Testing to ensure our code quality.
