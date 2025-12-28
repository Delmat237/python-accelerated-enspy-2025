# MOIS_2_POO_AVANCEE/INTRODUCTION_OOP.md : Introduction to OOP

## Introduction to Object-Oriented Programming (OOP)
### *Why OOP is essential for a professional Python developer*

---

### Why OOP?

| Real Problem | OOP Solution |
|---------------|--------------|
| Duplicated code, hard to maintain | **Reuse** via classes |
| Mixed data and behaviors | **Encapsulation**: data + methods |
| Complex system evolution | **Inheritance** and **Polymorphism** |
| Team projects (Flask, Django, APIs) | **Modularity** and **Readability** |

> **Concrete Example**: A pharmacy manages medicines, clients, invoices.  
> Without OOP → 50 global functions → nightmare.  
> With OOP → 3 clear classes → clean, evolvable, testable.

---

### The 4 Pillars of OOP

| Pillar | Definition | Example |
|--------|------------|--------|
| **Encapsulation** | Group data + methods in a class | `class Medicament: def __init__(self, nom, prix): ...` |
| **Abstraction** | Hide complexity, show essentials | `.sell()` method without exposing internal stock |
| **Inheritance** | Reuse code from a parent class | `class Antibiotic(Medicine): ...` |
| **Polymorphism** | Same interface, different behaviors | `.calculate_price()` different by type |

---

### Utility in Cameroonian Context

| Field | OOP Application |
|--------|------------------|
| **Health** | Hospital management system (Patient, Doctor, Prescription) |
| **Agriculture** | Crop tracking (Plot, Crop, Yield) |
| **Finance** | Mobile banking (Account, Transaction, Client) |
| **Education** | E-learning platform (Student, Course, Grade) |

> **Month 2 Goal**: Master OOP to **build robust, testable, and evolvable systems**.

---

### Simple Analogy: The Car

```python
class Car:
    def __init__(self, brand, max_speed):
        self.brand = brand
        self.max_speed = max_speed
        self.speed = 0  # internal state
    
    def accelerate(self, increment):
        self.speed = min(self.speed + increment, self.max_speed)
    
    def brake(self):
        self.speed = 0
```

- **Object** = a specific car (`my_toyota = Car("Toyota", 180)`)
- **Class** = the blueprint
- **Methods** = possible actions
- **Attributes** = characteristics

---

### OOP vs Functional Programming

| OOP | Functional |
|-----|---------------|
| **Mutable state** (objects) | **Immutable state** |
| **Classes + methods** | **Pure functions** |
| Ideal for **real-world modeling** | Ideal for **data processing** |

> **Python = multi-paradigm** → we combine both!

---

### Month 2 Roadmap: Advanced OOP

```bash
MOIS_2_POO_AVANCEE/
├── INTRODUCTION_OOP.md                 ← THIS COURSE
├── WEEK_1_Classes_Encapsulation.md
├── WEEK_2_Heritage_Polymorphisme.md
├── WEEK_3_Methodes_Classe_Statiques.md
├── WEEK_4_Tests_Unitaires_Pytest.md
├── cours_poo_avance.tex
├── tests/
│   └── test_banking_system.py
└── TP_Banking_System/
    └── bank_account.py
```

---

### By the End of Month 2, You Will Know How To:

- Model a real system with classes
- Protect your data with `@property`
- Reuse code with inheritance
- Test automatically with `pytest`
- Write **clean, professional, industrial** code

---

**Next Step**:  
> **WEEK 1: Classes and Encapsulation**  
> `class`, `__init__`, `@property`, setters/getters
