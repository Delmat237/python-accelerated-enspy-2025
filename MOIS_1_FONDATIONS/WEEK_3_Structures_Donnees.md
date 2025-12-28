# 🛠️ MOIS_1_FONDATIONS/WEEK_3_Structures_Donnees.md : WEEK 3: Data Structures

## 🎯 Session Objectives (2h - 2h30)

| Mode | Practical Objective | Validated Skills |
| :--- | :--- | :--- |
| **Security/Efficiency** | Manage lists and tuples. | Mastery of **mutability**. |
| **Modeling** | Represent a complex object with dictionaries. | Use of **dictionaries** (`dict`). |
| **Optimization** | Reduce lines with comprehensions. | Mastery of **Comprehensions**. |

-----

## 1. 📦 Sequences: Lists and Tuples (45 min)

### Challenge 1: Inventory Management

**Objective:** Use a list (mutable) and a tuple (immutable).

#### 📝 Guided Code: Mutability

```python
# --- Lists (Mutable) ---
inventory = ["Rotor X1", "Sensor Z", "Valve A"]
inventory.append("Filter H9")  # Addition
inventory.remove("Sensor Z")  # Deletion
print(f"Inventory: {inventory}")

# --- Tuples (Immutable) ---
coordinates = (48.8584, 2.2945)
# coordinates[0] = 49.0  # ERROR expected
lat, lon = coordinates  # Unpacking
print(f"Lat: {lat}, Lon: {lon}")
```

> [!IMPORTANT]
> **Deep Dive: Lists vs Tuples in memory**  
> Lists are dynamic arrays: Python reserves slightly more space than needed to allow for fast appends. Tuples are allocated with the exact fixed size, making them slightly lighter and faster to iterate over.

---

## 2. 🗺️ Mapping: Dictionaries (60 min)

### Challenge 2: Incident Report

**Objective:** Model with a dictionary including nested data.

#### 📝 Guided Code: Dictionaries

```python
report = {
    "id": "INC-2025",
    "severity": "High",
    "details": {
        "author": "Durand",
        "department": "Maintenance"
    },
    "actions": ["Isolate", "Diagnose"]
}

# Secure access via .get() to avoid KeyError
department = report.get("details", {}).get("department", "Unknown")
report["status"] = "In progress"

for key, value in report.items():
    print(f"{key}: {value}")
```

> [!TIP]
> **Pro Tip: Sets for Uniqueness**  
> If you have a list with duplicates `[1, 2, 2, 3]` and you want unique elements, use `set()`.  
> `uniques = list(set(my_list))`. This is one of the fastest ways in Python to deduplicate data.

---

## 3. ⚡ Efficiency: Comprehensions (60 min)

### Challenge 3: Transformation

**Objective:** Replace a loop with a comprehension.

#### 📝 Guided Code: List Comprehension

```python
grades = [10, 15, 8, 19, 11]
# Filter grades > 12 and add 1
final_grades = [n + 1 for n in grades if n > 12]
print(f"Optimized: {final_grades}")
```

> [!WARNING]
> **Common Pitfall: Shallow vs Deep Copy**  
> `list_a = [1, [2, 3]]`  
> `list_b = list_a.copy()`  
> If you modify `list_b[1][0] = 99`, then `list_a[1][0]` will change too!  
> *Solution:* For copying complex structures (lists within lists), use `import copy` then `copy.deepcopy()`.

---

## 🧪 EXTRA EXERCISES (To go further)

### Exercise 1: Word Frequency Analysis
Write a script that takes a sentence and counts the occurrence of each word using a dictionary.
*Example:* "the cat eats the rat" -> `{"the": 2, "cat": 1, ...}`

### Exercise 2: Premium Stock Management
1. Create a dictionary where the key is the product name and the value is another dictionary `{price: float, quantity: int}`.
2. Write a function that calculates the total value of the stock.
3. Write a single line (comprehension) that lists products that are out of stock (`quantity == 0`).

---

## ⏳ Session Conclusion (15 min)

  * **Review:** Why are dictionaries so fast? (Thanks to Hashing/Hash Maps which allow almost instantaneous access).
  * **Week 4 Preparation:** We will make our scripts indestructible with exception handling and file I/O.
