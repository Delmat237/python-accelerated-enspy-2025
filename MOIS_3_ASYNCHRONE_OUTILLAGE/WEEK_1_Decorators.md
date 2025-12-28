# MOIS_3_ASYNCHRONE_OUTILLAGE/WEEK_1_Decorators.md : WEEK 1: Decorators and Closures

## 🎯 Session Objectives (3h)

| Mode | Practical Objective | Validated Skills |
| :--- | :--- | :--- |
| **Foundations** | Understand functions as "first-class citizens". | Mastery of nested functions and **Closures**. |
| **Elegance** | Create simple decorators for logging. | `@decorator` syntax, `wraps`. |
| **Power** | Design decorators with arguments. | Maximum code flexibility. |

---

## 1. Closures: The DNA of Decorators (45 min)

Before understanding decorators, you must understand that a function can "capture" its environment.

### Challenge 1: The Memory Function

**Objective:** Create a function that remembers a configuration value.

#### 📝 Guided Code: Closures

```python
def create_multiplier(factor):
    def multiplier(n):
        return n * factor
    return multiplier

double = create_multiplier(2)
triple = create_multiplier(3)

print(double(10)) # 20
print(triple(10)) # 30
```

> [!IMPORTANT]
> **Deep Dive: What is a Closure?**  
> It's a function that "keeps alive" the variables of its parent function, even after the parent function has finished executing. Python stores this in a special attribute: `__closure__`.

---

## 2. Decorators: Modify without Touching (1h15)

A decorator is a function that takes another function and "decorates" it with new behavior.

### Challenge 2: Function Timer

**Objective:** Automatically measure the execution time of a function.

#### 📝 Guided Code: `@decorator`

```python
import time
from functools import wraps

def timer(func):
    @wraps(func) # <-- Crucial to keep original function metadata
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        end = time.perf_counter()
        print(f"⏱️ {func.__name__} execution time: {end - start:.4f}s")
        return result
    return wrapper

@timer
def download_data():
    time.sleep(1.5)
    print("Data received.")

download_data()
```

> [!TIP]
> **Pro Tip: The Importance of `functools.wraps`**  
> Without `@wraps`, the decorated function would lose its name and docstring (`download_data.__name__` would become "wrapper"). Use it systematically.

---

## 3. Decorators with Arguments (1h)

Sometimes, we want to pass options to our decorator itself.

### Challenge 3: Retry Limiter

**Objective:** Create a decorator that limits the number of times a function can be run.

#### 📝 Guided Code: Triple nesting

```python
def limit_retries(max_tries):
    def decorator(func):
        tries = 0
        @wraps(func)
        def wrapper(*args, **kwargs):
            nonlocal tries # Allows modifying the closure variable
            if tries < max_tries:
                tries += 1
                return func(*args, **kwargs)
            else:
                print(f"❌ Error: {func.__name__} has reached its limit.")
        return wrapper
    return decorator

@limit_retries(max_tries=3)
def send_email():
    print("Email sent!")

send_email() # OK
send_email() # OK
send_email() # OK
send_email() # BLOCKED
```

---

## 🧪 EXTRA EXERCISES (To go further)

### Exercise 1: Security Logger
Create a `@logger` decorator that records the time and name of every called function into a `security.log` file.

### Exercise 2: Results Cache (Memoization)
Create a decorator that stores the result of a function for a given argument in a dictionary. If the function is called with the same argument, return the cached value instead of recalculating. (Hint: perfect for the Fibonacci sequence!).

---

## ⏳ Session Conclusion (15 min)

  * **Review:** Why are decorators everywhere in frameworks (FastAPI, Flask, Pytest)? (Because they allow a clean separation between business logic and cross-cutting tools like auth or logging).
  * **Week 2 Preparation:** We will discover how Python handles waiting with Asynchrony (`asyncio`).
