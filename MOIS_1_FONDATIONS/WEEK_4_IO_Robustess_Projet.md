# 🛠️ MOIS_1_FONDATIONS/WEEK_4_IO_Robustesse_Projet.md : WEEK 4: I/O, Robustness and Final Project

## 🎯 Session Objectives (2h - 2h30)

| Mode | Practical Objective | Validated Skills |
| :--- | :--- | :--- |
| **I/O** | Read and write data in files with secure management. | Mastery of `with open()`, `pathlib`. |
| **Robustness** | Handle real-world error scenarios. | `try/except/finally` blocks and custom exceptions. |
| **Project** | Develop an integrated stock simulator. | Synthesis of skills (OOP, I/O, Random). |

-----

## 1. 📝 Input/Output: File Management (60 min)

### Challenge 1: Transaction Logging

**Objective:** Create a script that writes transactions to a file.

#### 📝 Guided Code: `with open()` and `pathlib`

```python
from pathlib import Path

# Using pathlib (Modern way vs os.path)
data_folder = Path("data")
data_folder.mkdir(exist_ok=True) # Creates the folder if it doesn't exist
file_path = data_folder / "transaction_log.txt"

transactions = ["Buy: 100 shares @ 50€", "Sell: 50 shares @ 55€"]

# --- Writing ---
with open(file_path, "w", encoding="utf-8") as file:
    for t in transactions:
        file.write(t + "\n")

print(f"File saved at: {file_path.absolute()}")
```

> [!IMPORTANT]
> **Deep Dive: Why the `with` block?**  
> The `with` keyword uses a **Context Manager**. It guarantees that `file.close()` is called automatically, even if an error occurs during writing. Without it, you risk corrupting the file or leaking system resources.

---

## 2. 🛡️ Robustness: Error Handling (60 min)

### Challenge 2: Advanced Error Handling

**Objective:** Handle missing files and invalid inputs with professional messages.

#### 📝 Guided Code: `try/except/finally`

```python
def read_data(filename):
    try:
        with open(filename, "r") as f:
            return f.readlines()
    except FileNotFoundError:
        print(f"❌ Error: File '{filename}' was not found.")
    except Exception as e:
        print(f"⚠️ Unexpected error: {e}")
    finally:
        print("Reading operation attempted.") # Always executes

entries = read_data("non_existent.txt")
```

> [!TIP]
> **Pro Tip: Custom Exceptions**  
> You can define your own errors to make your code more explicit:  
> `class InsufficientBalanceError(Exception): pass`  
> This allows you to: `raise InsufficientBalanceError("You don't have enough money.")`.

---

## 🎲 Integration Project: Stock Simulator (60 min)

### Challenge 3: Smart Stock Simulator

**Objective:** Generate prices, save them, and handle reading errors.

#### 📝 Guided Code: Integration

```python
import random

def simulate_market(num_days=5):
    history = []
    for day in range(1, num_days + 1):
        price = round(random.uniform(50, 150), 2)
        history.append(f"Day {day}: {price}€")
    
    try:
        with open("market.txt", "w") as f:
            f.write("\n".join(history))
        print("✅ Simulation saved.")
    except IOError:
        print("❌ Could not write to disk.")

simulate_market()
```

> [!WARNING]
> **Common Pitfall: Catching all exceptions**  
> Avoid using a bare `except:` without specifying the error type. This will catch even `Ctrl+C` (KeyboardInterrupt), making your program impossible to stop manually. Always specify `except ValueError:`, `except FileNotFoundError:`, etc.

---

## 🧪 EXTRA EXERCISES (To go further)

### Exercise 1: Log File Cleaner
Create a script that reads a text file, removes empty lines, and saves the result into a new file `clean_log.txt`.

### Exercise 2: Auto-Backup System
Use `pathlib` to list all `.txt` files in a folder and copy them to a `backup/` folder, adding the `backup_` prefix to their names.

---

## ⏳ Session Conclusion (15 min)

  * **Review:** Why is robustness more important than pure functionality? (Crashing code is unusable code, no matter how powerful).
  * **End of Month 1:** Congratulations! You have mastered the foundations.
  * **Month 2:** Get ready to enter the world of **Object-Oriented Programming (OOP)**.
