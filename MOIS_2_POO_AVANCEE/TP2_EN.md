# 🎓 TP 2 - Month 2: OOP and Architecture (Complete Exam)

## 🎯 TP Objectives (3h)

This TP evaluates your ability to design a robust software architecture using the pillars of OOP: Encapsulation, Inheritance, Polymorphism. You will also have to validate your code through automated unit tests.

---

## 1. Encapsulation: Hospital Management (45 min)
**Scenario:** Design a `Patient` class for a hospital in Yaoundé.

- Private attributes: `__id`, `__name`, `__medical_record` (list).
- Use `@property` to access the name.
- Implement a setter for the name that checks that it is not empty.
- Method `add_diagnosis(info)` to fill the record.

```python
class Patient:
    def __init__(self, patient_id, name):
        # Your code here...
```

---

## 2. Inheritance and Polymorphism: Transport Fleet (1h)
**Scenario:** A Cameroonian travel agency manages different types of vehicles.

- Parent Class: `Vehicle` with `calculate_fare(distance)` method.
- Sub-classes: `Bus` and `VIPCar`.
- `Bus`: Fixed rate of 500 FCFA/km.
- `VIPCar`: Rate of 1200 FCFA/km + on-board service (2000 FCFA).
- Use `super()` in constructors.

---

## 3. Class and Static Methods: Financial Management (30 min)
**Scenario:** Create a `BankAccount` class.

- Class attribute: `interest_rate = 0.03`.
- Class method: `change_rate(new_rate)`.
- Static method: `is_valid_number(number)` (checks if 10 digits).

---

## 4. Unit Testing: Calculation Validation (45 min)
**Scenario:** Test your transport system with `pytest`.

- Create a fixture for a `Bus`.
- Test the fare calculation for a normal distance.
- Test that the fare cannot be negative (raise a `ValueError`).

---

## 🏆 Final Project: Library Management System (1h)
**Instructions:**
Create a system with:
1. A `Book` class (Encapsulation).
2. A `DigitalBook` class that inherits from `Book`.
3. A `Library` class that manages a list of books.
4. A test file `test_library.py` validating adding and borrowing.

---

## 🚀 Submission Procedure (Git)

1. **Clone the repository:**
   `git clone https://github.com/club-genie-informatique-enspy/TP-PYTHON-TRAINING.git`
2. **Create a branch:**
   `git checkout -b tp_python/tp2-<your-last-name>-<your-first-name>`
3. **Commit:**
   `git commit -m "tp_python(tp2): add hospital and transport management"`
4. **Push & PR:**
   Send to GitHub and create a **Pull Request** to `main`.
