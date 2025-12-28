# 🛠️ MOIS_1_FONDATIONS/WEEK_2_Boucles_Fonctions.md : WEEK 2: Loops and Functions

## 🎯 Session Objectives (2h - 2h30)

| Mode | Practical Objective | Validated Skills |
| :--- | :--- | :--- |
| **Automation** | Process lists or simulate an iterative process. | Mastery of **`for`**, **`while`**, **`range()`**, **`break`/`continue`**. |
| **Modularity** | Create reusable and documented code blocks. | Use of **`def`**, **`return`**, **named arguments** (PEP 257). |
| **Advanced** | Function accepting variable arguments. | Introduction to **`*args`** and **Scope**. |

-----

## 1. 🔄 Automation: Loops (60 min)

Loops allow you to execute repetitive tasks efficiently.

### Challenge 1: Production Tracking

**Objective:** Simulate 10 batch inspections with `break` and `continue`.

#### 📝 Guided Code: `for`, `break` and `continue`

```python
# States: (1: OK, 0: Defective, -1: Skipped)
inspection_states = [1, 1, 0, 1, -1, 1, 1, 0, 1, 1]

print("--- Quality Control Start ---")

for batch_number, status in enumerate(inspection_states, start=1):
    if status == 0:
        print(f"❌ Batch n°{batch_number}: DEFECTIVE. Stopping (break).")
        break
    if status == -1:
        print(f"⚠️ Batch n°{batch_number}: Missed inspection. Skipping (continue).")
        continue
    print(f"✅ Batch n°{batch_number}: Compliant.")

print("--- Quality Control End ---")
```

#### 💡 Detailed Theory: Iteration

| Concept | `for` (Iterator) | `while` (Conditional) |
| :--- | :--- | :--- |
| **Usage** | Browse an **iterable** (`list`, `range`). | While a condition is true. |
| **Risk** | Low. | High (infinite loops). |
| **`range()`** | Sequence generated on-the-fly (efficient). | n/a |

> [!WARNING]
> **Common Pitfall: Modifying a list during iteration**  
> Avoid deleting items from a list you are directly looping over with `for`. This shifts indices and causes items to be skipped.  
> *Solution:* Loop over a copy `for item in my_list[:]:` or use a list comprehension.

---

## 2. 🧱 Modularity: Functions (75 min)

Functions encapsulate logic, making it easy to maintain.

### Challenge 2: Profitability Calculator

**Objective:** Create a documented function calculating net profit.

#### 📝 Guided Code: `def`, `return` and `docstrings`

```python
def calculate_net_profit(income: float, expenses: float, tax_rate: float = 0.25) -> float:
    """
    Calculates net profit after taxes.

    Args:
        income (float): Total gross income.
        expenses (float): Total expenses.
        tax_rate (float, optional): Tax rate (default 0.25).

    Returns:
        float: The calculated net profit.
    """
    if income < 0 or expenses < 0:
        raise ValueError("Amounts cannot be negative.")
        
    gross_profit = income - expenses
    return gross_profit * (1 - tax_rate)

# Calls with named arguments for clarity
res = calculate_net_profit(income=100000, expenses=30000, tax_rate=0.30)
print(f"Net Profit: {res:.2f}€")
```

> [!TIP]
> **Pro Tip: Type Hinting**  
> Use `:` and `->` (as shown above) to indicate expected types. This doesn't block execution but helps IDEs (like VSCode) suggest methods and catch errors before running your code.

---

## 3. 🧠 Advanced: `*args` and Scope (30 min)

### Challenge 3: Flexible Calculator

**Objective:** Use **`*args`** for a variable grades count.

#### 📝 Guided Code: `*args`

```python
def calculate_average(subject: str, *grades: float):
    if not grades:
        return 0
    return sum(grades) / len(grades)

print(f"Math Average: {calculate_average('Math', 12, 14, 16):.2f}")
```

> [!IMPORTANT]
> **Deep Dive: The LEGB Rule (Scope)**  
> Python looks for variables in this order:  
> 1. **L**ocal: Inside the current function.  
> 2. **E**nclosing: In the parent function (if nested).  
> 3. **G**lobal: At the file level.  
> 4. **B**uilt-in: Python's core functions (e.g., `len`, `sum`).

---

## 🧪 EXTRA EXERCISES (To go further)

### Exercise 1: Guess the Number
Create a game where the computer chooses a number between 1 and 100.
Use a `while` loop to ask the user to guess.
Provide hints "Higher" or "Lower" until they find it.

### Exercise 2: Fibonacci Sequence
Write a function that generates the first `n` numbers of the Fibonacci sequence.
*Reminder:* Each number is the sum of the two preceding ones (0, 1, 1, 2, 3, 5, 8...).

---

## ⏳ Session Conclusion (15 min)

  * **Review:** Why prefer functions over long scripts? (Reusability, testability, readability).
  * **Week 3 Preparation:** We will see how to organize complex masses of data with Dictionaries.
