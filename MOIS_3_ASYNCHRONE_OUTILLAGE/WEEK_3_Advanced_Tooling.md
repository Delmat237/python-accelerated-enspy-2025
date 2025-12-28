# MOIS_3_ASYNCHRONE_OUTILLAGE/WEEK_3_Advanced_Tooling.md : WEEK 3: Advanced Tooling and Logging

## 🎯 Session Objectives (3h)

| Mode | Practical Objective | Validated Skills |
| :--- | :--- | :--- |
| **Monitoring** | Replace `print()` with the `logging` module. | Log levels, formatters, handlers. |
| **Security** | Manage secrets with `.env` files. | `python-dotenv` library. |
| **Robustness** | Create a global error handling system. | Advanced use of `sys.excepthook`. |

---

## 1. Logging: See what your code is doing (1h15)

In production, you cannot see the user's screen. Logging writes the history of your program into a file.

### Challenge 1: Pro Logger Configuration

**Objective:** Create a system that writes errors to a file and info to the console.

#### 📝 Guided Code: `logging`

```python
import logging

# 1. Create the logger
logger = logging.getLogger("MyApp")
logger.setLevel(logging.DEBUG)

# 2. Create handlers (Destinations)
console_handler = logging.StreamHandler()
file_handler = logging.FileHandler("app.log")

# 3. Create an elegant format
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
console_handler.setFormatter(formatter)
file_handler.setFormatter(formatter)

# 4. Add handlers to the logger
logger.addHandler(console_handler)
logger.addHandler(file_handler)

# Tests
logger.info("Application started.")
logger.warning("Warning: disk space is low.")
logger.error("Critical error: database connection failed.")
```

> [!IMPORTANT]
> **Deep Dive: Log Levels**  
> - `DEBUG`: Technical details for development.
> - `INFO`: Confirmation that everything is going as planned.
> - `WARNING`: Something unexpected, but the app is still running.
> - `ERROR`: A serious problem, a feature has failed.
> - `CRITICAL`: The entire application might stop.

---

## 2. Environment Variables: Never hardcode passwords (45 min)

### Challenge 2: Securing access

**Objective:** Use `.env` to store an API key.

#### Steps:
1. Install: `pip install python-dotenv`
2. Create a `.env` file: `API_KEY=your_secret_key_123`

#### 📝 Guided Code: `dotenv`

```python
import os
from dotenv import load_dotenv

load_dotenv() # Loads the .env file into memory

api_key = os.getenv("API_KEY")

if api_key:
    print(f"✅ API Key loaded: {api_key[:4]}****")
else:
    print("❌ Error: API Key not found in .env")
```

> [!TIP]
> **Pro Tip: `.gitignore`**  
> **Never** forget to add `.env` to your `.gitignore` file so you don't send your secret access to GitHub!

---

## 3. Global Error Handling (1h)

In addition to `try/except`, we can capture all errors that might have been missed.

#### 📝 Guided Code: `excepthook`

```python
import sys

def global_error_handler(err_type, err_value, err_traceback):
    logger.critical(f"UNCAUGHT EXCEPTION: {err_value}", exc_info=(err_type, err_value, err_traceback))

sys.excepthook = global_error_handler

# Test a crash
1 / 0
```

---

## 🧪 EXTRA EXERCISES (To go further)

### Exercise 1: Log Rotation
Use `RotatingFileHandler` so your log file never exceeds 1MB, keeping the last 5 files.

### Exercise 2: Config Validator
Create a script that checks at startup if all necessary variables (DATABASE_URL, SECRET_KEY) are present in the `.env` and refuses to start if one is missing.

---

## ⏳ Session Conclusion (15 min)

  * **Review:** Why is `print()` banned in a professional environment? (Impossible to filter, doesn't record anything permanently, slows down display).
  * **Week 4 Preparation:** The Big Project! We're building an ultra-powerful asynchronous Web Scraper.
