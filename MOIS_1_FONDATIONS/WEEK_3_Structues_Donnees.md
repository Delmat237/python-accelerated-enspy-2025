# 🛠️ MOIS_1_FONDATIONS/WEEK_3_Structures_Donnees.md : WEEK 1: Data Structures

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

#### 💡 Brief Theory

  * **Lists:** Mutable, ideal for dynamic data.
  * **Tuples:** Immutable, optimized for security and speed.

-----

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

# Secure access
department = report.get("details", {}).get("department", "Unknown")
report["status"] = "In progress"

for key, value in report.items():
    print(f"{key}: {value}")
```

### 🧪 EXPRESS Lab: Merging (15 min)

**Task:** Merge two dictionaries.

```python
base_info = {"name": "Kamga"}
extra_params = {"city": "Douala"}
full_info = base_info | extra_params  # Merge operator
print(full_info)
```

-----

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

#### 📝 Guided Code: Dictionary

```python
products = [("X1", 120), ("Y2", 45)]
clean_inventory = {k: v for k, v in products if v >= 50}
print(clean_inventory)
```

-----

## ⏳ Session Conclusion (15 min)

  * **Review:** Comprehension performance.
  * **Week 4 Preparation:** Error handling (`try/except`).
