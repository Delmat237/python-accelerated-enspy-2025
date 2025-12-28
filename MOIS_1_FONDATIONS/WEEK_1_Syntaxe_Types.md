# 🛠️ MOIS_1_FONDATIONS/WEEK_1_Syntaxe_Types.md : WEEK 1: Syntax and Types

## 🎯 Session Objectives (2h - 2h30)

| Mode | Practical Objective | Validated Skills |
| :--- | :--- | :--- |
| **Setup** | Start a Python project from scratch. | Professional environment configuration. |
| **Code-First** | Implement a conversion script. | Mastery of types and operators. |
| **Logic** | Write an access verification function. | Use of booleans and conditions. |

-----

## 1. 🚀 Startup and Environment (30 min)

### Challenge 1: Setting up the Workshop

**Objective:** Create an isolated environment and follow the coding standard from the start.

#### Steps (To be executed directly)

1.  Open your terminal and create your work folder:
    `mkdir MOIS_1_FONDATIONS && cd MOIS_1_FONDATIONS`
2.  Create the virtual environment and activate it:
    `python -m venv .venv` followed by `source .venv/bin/activate` (Linux/Mac) or `.venv\Scripts\activate` (Windows).
3.  Create the first file: `touch WEEK_1_Syntaxe_Types.py`.
4.  In this file, define a variable following **PEP 8 (snake_case)**:
    ```python
    # Compliant variable name (PEP 8): 
    project_name = "Stock Simulator"
    # NON-compliant variable name:
    # ProjectName = "..." 
    ```

#### 💡 Detailed Theory: Environment and Standards (PEP 8)

| Concept | Detailed Explanation | Coder's Rule |
| :--- | :--- | :--- |
| **`venv`** | Isolates the project from the global Python install. Prevents library conflicts. | **Mandatory.** Always activate `venv` before installing dependencies. |
| **PEP 8** | Official style guide for **consistency**. Readable code is cheaper to maintain. | **Top Priority.** Use `snake_case`. **Always indent with 4 spaces.** |
| **The Interpreter** | Python is an **interpreted** language. Code is executed line by line. | type `python filename.py` to run. |

> [!TIP]
> **Pro Tip:** Use descriptive variable names. Avoid `a`, `b`, `c`. Prefer `user_age` or `unit_price`. Your future self will thank you when debugging!

---

## 2. 🧮 Data Types and Operators (60 min)

### Challenge 2: The Smart Converter

**Objective:** Write a script that converts seconds into `H:M:S` format using **`f-string`**.

#### 📝 Guided Code: The Solution

```python
# 1. Input data
total_duration_seconds = 9876 

# 2. Calculation of Hours, Minutes, Seconds
hours = total_duration_seconds // 3600  
remaining_seconds = total_duration_seconds % 3600

minutes = remaining_seconds // 60      
seconds = remaining_seconds % 60

# 3. Professional output (F-string)
print(f"Total duration: {hours}h {minutes}m {seconds}s")
```

#### 💡 Detailed Theory: Arithmetic and Typing

| Concept | Explanation | Implication |
| :--- | :--- | :--- |
| **Strong Typing** | Python forbids operations between incompatible types (e.g., `"5" + 2`). | You must explicitly convert: `int("5") + 2`. |
| **Dynamic Typing** | A variable can change type during execution. | Total flexibility, but watch out for logic errors. |
| **`//` vs. `/`** | **`/`** (classic division) always yields a `float`. **`//`** (floor division) yields an `int`. | Crucial for indexing or whole counts. |

> [!IMPORTANT]
> **Deep Dive: Memory and `id()`**  
> In Python, everything is an object. You can see the memory address of a variable using `id(variable_name)`.  
> `x = 10` -> `id(x)` will give the location of the integer 10. If you do `y = 10`, `id(y)` will often be the same because Python optimizes small integers (interning).

---

## 3. 🚦 Conditional Logic (60 min)

### Challenge 3: The Secure Access Guard

**Objective:** Check access rights based on status and license.

#### 📝 Guided Code: The `if/elif` Solution

```python
# Input variables
status = "Admin"
license_active = False
security_level = 4 

# Access gate logic
if status == "Admin" and security_level >= 5:
    print("✅ PREMIUM ADMINISTRATOR ACCESS.")
elif status == "Admin" or security_level == 4:
    print("⚠️ Standard administrator or level 4 access.")
elif not license_active: 
    print("❌ ACCESS DENIED. Inactive license.")
else:
    print("Status error.")
```

> [!WARNING]
> **Common Pitfall: Short-circuit Evaluation**  
> In an `and` statement, if the first condition is `False`, Python doesn't evaluate the second.  
> In an `or` statement, if the first is `True`, it stops there.  
> *Consequence:* Place "cheaper" or more likely conditions first to optimize execution.

---

## 🧪 EXTRA EXERCISES (To go further)

### Exercise 1: Number Analysis
Ask the user for a number (via `input()`). 
1. Check if it's even or odd (hint: use `% 2`).
2. Check if it's positive, negative, or zero.
3. Display a complete summary message.

### Exercise 2: BMI Calculator (Body Mass Index)
1. Create variables `weight` (kg) and `height` (m).
2. Calculate BMI: `weight / (height ** 2)`.
3. Display the category according to WHO:
   - < 18.5: Underweight
   - 18.5 to 25: Normal
   - > 25: Overweight

---

## ⏳ Session Conclusion (15 min)

  * **Code Review:** Why is indentation mandatory in Python? (Answer: It defines code blocks).
  * **Week 2 Preparation:** We will learn to repeat actions without copy-pasting (Loops).
