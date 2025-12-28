# 🎓 TP 3 - Month 3: Advanced Python and Asynchrony (Complete Exam)

## 🎯 TP Objectives (3h)

This TP evaluates your mastery of advanced Python concepts necessary for high-performance system development and professional project management.

---

## 1. Decorators and Closures: Security and Performance (45 min)
**Scenario:** You are working for a Fintech startup in Douala.

- Create a `generate_transaction_id(prefix)` closure that returns a function generating successive IDs (e.g., TX-1, TX-2).
- Create a `@verify_admin` decorator that checks if a global variable `is_admin` is set to `True`.
- Create a `@timeout(seconds)` decorator that warns if a function exceeds a time limit.

```python
# Base example
is_admin = False

def verify_admin(func):
    # Your code here...
```

---

## 2. Asynchronous Programming: Price Scraper (1h)
**Scenario:** Simulate fetching cocoa prices from 3 different markets in parallel.

- Use `asyncio` and `async/await`.
- Use `asyncio.gather` for simultaneity.
- Handle failures with `try/except` (simulate 50% errors).

---

## 3. Advanced Tooling: Logging and Configuration (30 min)
- Configure a `logger` to `errors.log` and the console.
- Load your constants (URL, retries) from a `.env` file.
- Log fatal errors via `sys.excepthook`.

---

## 4. Multi-threading: Data Processing (45 min)
- Use `ThreadPoolExecutor` to simulate processing multiple I/O-bound tasks.
- Compare the time gain compared to sequential mode.

---

## 🏆 Final Project: Monitoring Micro-Service (1h)
**Instructions:**
Create a complete script unifying these concepts:
1. Configuration through `.env`.
2. Logging and timing decorators.
3. Asynchronous URL checking.
4. Final report in a log file.

---

## 🚀 Submission Procedure (Git)

1. **Clone the repository:**
   `git clone https://github.com/club-genie-informatique-enspy/TP-PYTHON-TRAINING.git`
2. **Create a branch:**
   `git checkout -b tp_python/tp3-<your-last-name>-<your-first-name>`
3. **Commit:**
   `git commit -m "tp_python(tp3): add monitoring micro-service and decorators"`
4. **Push & PR:**
   Send to GitHub and create a **Pull Request** to `main`.
