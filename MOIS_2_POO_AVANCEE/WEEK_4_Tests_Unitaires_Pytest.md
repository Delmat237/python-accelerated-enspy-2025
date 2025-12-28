# MOIS_2_POO_AVANCEE/WEEK_4_Tests_Unitaires_Pytest.md : WEEK 4: Unit Testing with Pytest

## Learning Objectives (3h)

| Objective | Why is it crucial? |
|---------|--------------------------|
| **Understanding Unit Tests** | Check that each small block of code works in isolation. |
| **Using `pytest`** | Automate the verification of your classes professionally. |
| **The AAA Pattern** | Organize your tests in a readable and standardized way. |
| **Doing TDD (Test Driven Development)** | Write the test *before* the code for better design. |

---

## 1. Why Test? (30 min)

Tests ensure that your changes haven't broken existing functionalities (non-regression). They also serve as living documentation.

> [!IMPORTANT]
> **Deep Dive: The AAA Pattern (Arrange, Act, Assert)**
> Every good test follows this order:
> 1. **Arrange**: Set up the data (e.g., create an account with 100€).
> 2. **Act**: Execute the action to test (e.g., withdraw 50€).
> 3. **Assert**: Verify the result (e.g., is the balance exactly 50€?).

---

## 2. Testing Our Classes with Pytest (1h30)

### Challenge 1: My First Fixture

A **fixture** is a function that sets up an object to be used across multiple tests.

```python
import pytest
from bank_account import BankAccount

@pytest.fixture
def empty_account():
    return BankAccount("Tester", 0)

def test_valid_deposit(empty_account):
    # Act
    empty_account.deposit(500)
    # Assert
    assert empty_account.balance == 500
```

> [!TIP]
> **Pro Tip: Parametrization**  
> Instead of writing 5 tests to check 5 different amounts, use `@pytest.mark.parametrize`.  
> This allows you to run the same test with a list of input values and expected results.

---

## 3. Testing Errors (30 min)

It is just as important to test that your code *fails* when it's supposed to.

#### 📝 Guided Code: `pytest.raises`

```python
def test_negative_deposit(empty_account):
    with pytest.raises(ValueError, match="Positive amount required"):
        empty_account.deposit(-10)
```

---

## 4. Integration Lab: Total Coverage (1h)

**Objective:** Reach 100% test coverage for the `SavingsAccount` class.

> [!WARNING]
> **Common Pitfall: Side Effects**  
> If your test creates a file on the disk, make sure it deletes it afterward (or use Pytest's `tmp_path` fixtures). A test should never leave "mess" behind, otherwise subsequent tests might fail because of it.

---

## 🧪 EXTRA EXERCISES (To go further)

### Exercise 1: Calculator Test
Go back to your `calculate_average` function from Week 2.
Write tests for:
1. A normal list of grades.
2. An empty list (should return 0 or raise an error depending on your choice).
3. A negative grade.

### Exercise 2: Zoo Fixture
Create a `populated_zoo` fixture that returns a list containing a `Dog` and a `Cat`.
Test that the `make_everyone_speak` method works correctly on this fixture.

---

## ⏳ Conclusion of Month 2

Congratulations! You have transformed your way of coding: from simple scripts to a **complete, secure, and tested object-oriented system**.

  * **Review:** Why are tests called an investment? (You save time in the long run by avoiding repetitive bugs).
  * **Next Step:** Month 3 will cover Databases (SQL) to persist your objects!
