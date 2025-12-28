# 🎓 TP 1 - Month 1: Foundations (Complete Exam)

## 🎯 TP Objectives (2h - 3h)

This sheet offers concrete exercises inspired by real everyday problems or engineering fields in Cameroon (e.g., agricultural management, health, local finance, education). The approach is **practical and code-first**: each exercise simulates a professional scenario to apply the concepts.

**Required Material:** Python 3.11+, IDE (VS Code).

---

## 1. Data Types: Real Agricultural Calculations (20 min)

### Exercise 1: Seed Cost
**Real Context:** In Cameroon, a farmer calculates the cost of seeds for a maize plot.

- Declare `bags_quantity` (int), `price_per_bag` (float), `crop` (str).
- Calculate the total (`bags_quantity * price_per_bag`).
- Display a formatted message: "The cost for X bags of Y seeds is Z FCFA."

```python
bags_quantity = 5
price_per_bag = 15000.50
crop = "maize"
# Your code here...
```

### Exercise 2: Unit Conversion
- Convert an area in hectares (float) to m² (int).
- Handle an error if the area is negative.

---

## 2. Conditions and Logic: Social Aid Eligibility (20 min)

### Exercise 3: Eligibility Verification
**Real Context:** Verify social aid eligibility based on income, number of children, and status (rural/urban).

- If `income < 100000` FCFA **AND** `num_children > 2` **OR** `is_rural`, display "Eligible for aid".
- Otherwise, "Not eligible".

```python
monthly_income = float(input("Monthly income (FCFA): "))
num_children = int(input("Number of children: "))
is_rural = input("Rural area? (yes/no) ") == "yes"
# Your code here...
```

---

## 3. Loops: Daily Harvest Tracking (30 min)

### Exercise 5: Daily Tracking
**Real Context:** 7-day harvest tracking with alerts.

- Use `for` with `range(1, 8)`.
- Generate a random yield (`random.randint(50, 200)` kg/day).
- If `yield < 100`, skip to the next (`continue`).
- If `yield < 50`, stop everything (`break`) with an alert.

---

## 4. Functions: Family Budget Tool (30 min)

### Exercise 7: Budget Calculation
**Real Context:** Monthly budget calculation (Food, Transport, Education).

- Define `calculate_budget(food, transport, *others)`.
- Return the total sum.

---

## 5. Data Structures: Inventory Management (30 min)

### Exercise 9: List and Dictionary
- Create a list of medicines.
- Create a dictionary for medicine details (name, price, quantity).

---

## 🏆 Integrative Project: Harvest Management System (30 min)

**Scenario:** A farmer tracks cocoa harvests over 5 days, calculates the average, identifies low-yield days (< 100kg), and stores everything in a dictionary.

---

## 🚀 Submission Procedure (Git)

1. **Clone the repository:**
   `git clone https://github.com/club-genie-informatique-enspy/TP-PYTHON-TRAINING.git`
2. **Create a branch:**
   `git checkout -b tp_python/tp1-<your-last-name>-<your-first-name>`
3. **Commit:**
   `git commit -m "tp_python(tp1): add harvest management system"`
4. **Push & PR:**
   Send to GitHub and create a **Pull Request** to `main`.
