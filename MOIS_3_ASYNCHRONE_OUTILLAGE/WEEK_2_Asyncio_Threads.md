# MOIS_3_ASYNCHRONE_OUTILLAGE/WEEK_2_Asyncio_Threads.md : WEEK 2: Asyncio and Multi-threading

## 🎯 Session Objectives (3h)

| Mode | Practical Objective | Validated Skills |
| :--- | :--- | :--- |
| **Concept** | Understand the difference between synchronous and asynchronous. | Restaurant analogy, event loop. |
| **Asynchrony** | Use `async`, `await`, and `gather`. | Mastery of the `asyncio` library. |
| **Parallelism** | Know when to use Multi-threading. | Use of `ThreadPoolExecutor`. |

---

## 1. Analogy: The Asynchrony Restaurant (30 min)

Imagine a waiter in a restaurant:
- **Synchronous:** The waiter takes an order, goes to the kitchen, and waits for the dish to be ready before serving the customer and moving to the next. (Waste of time!)
- **Asynchronous:** The waiter takes the order, gives it to the kitchen, and goes to take another order while waiting for the first dish to be ready. (Maximum efficiency!)

---

## 2. Asyncio: The Magic of Waiting (1h15)

`asyncio` is the heart of asynchronous programming in Python.

### Challenge 1: Mock Web Requests

**Objective:** Download multiple "pages" simultaneously without blocking the program.

#### 📝 Guided Code: `async/await`

```python
import asyncio
import time

async def mock_request(name, delay):
    print(f"🚀 Starting request {name}...")
    await asyncio.sleep(delay) # <-- We wait without blocking
    print(f"✅ Request {name} finished after {delay}s")
    return f"Result {name}"

async def main():
    start = time.perf_counter()
    
    # SIMULTANEOUS launch
    results = await asyncio.gather(
        mock_request("A", 2),
        mock_request("B", 1),
        mock_request("C", 1.5)
    )
    
    end = time.perf_counter()
    print(f"\nTotal time: {end - start:.2f}s")
    print(f"Results: {results}")

if __name__ == "__main__":
    asyncio.run(main())
```

> [!IMPORTANT]
> **Deep Dive: The Event Loop**  
> Python uses a single execution thread but switches from one task to another as soon as an `await` is encountered. The Event Loop manages this ultra-fast scheduling.

---

## 3. Multi-threading: When Asyncio is not Enough (1h)

Asynchrony is perfect for **I/O (network, files)**. But for heavy computations (CPU), we need Multi-threading or Multi-processing.

### Challenge 2: Parallel File Processing

#### 📝 Guided Code: `ThreadPoolExecutor`

```python
from concurrent.futures import ThreadPoolExecutor
import time

def heavy_task(n):
    print(f"🔨 Calculation for {n} started...")
    time.sleep(1) # Simulates a calculation
    return n * n

with ThreadPoolExecutor(max_workers=3) as executor:
    numbers = [1, 2, 3, 4, 5]
    results = list(executor.map(heavy_task, numbers))

print(f"Final results: {results}")
```

> [!WARNING]
> **Common Pitfall: The GIL (Global Interpreter Lock)**  
> In Python, two threads cannot execute Python code at the same time on the same CPU. Multi-threading is therefore useful for waiting (I/O) but not for speeding up pure mathematical calculations (use `multiprocessing` for that).

---

## 🧪 EXTRA EXERCISES (To go further)

### Exercise 1: Asynchronous Port Scanner
Write an `asyncio` script that attempts to connect to a list of ports (80, 443, 22) on a test server to see if they are open.

### Exercise 2: Speed Comparison
Create a script that downloads the same URL 5 times (use a dummy delay):
1. Classically (synchronous).
2. With `asyncio.gather`.
Display the time difference.

---

## ⏳ Session Conclusion (15 min)

  * **Review:** When to use `asyncio`? (When you have a lot of network/disk waiting).
  * **Week 3 Preparation:** We will see how to monitor our programs with professional Logging.
