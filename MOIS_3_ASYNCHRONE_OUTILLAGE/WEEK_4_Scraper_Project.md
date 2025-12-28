# MOIS_3_ASYNCHRONE_OUTILLAGE/WEEK_4_Scraper_Project.md : WEEK 4: Project – Asynchronous Web Scraper

## 🎯 Final Project Objective
Build a scraper capable of fetching information from multiple web pages in parallel, with error handling, logging, and environment-based configuration.

---

## 🏗️ Project Architecture

The project will be structured as follows:
```bash
Scraper_Project/
├── .env                # Keys and configuration
├── .gitignore          # Exclusion of .env
├── app.log             # Operations history
├── main.py             # Heart of the program
└── requirements.txt    # httpx, python-dotenv
```

---

## 🚀 Step 1: Configuration (30 min)

**Objective:** Prepare the environment.

#### `requirements.txt`
```text
httpx
python-dotenv
```

#### `.env`
```text
BASE_URL=https://jsonplaceholder.typicode.com/posts
MAX_CONCURRENT_REQUESTS=5
```

---

## 🛠️ Step 2: Asynchronous Code (1h30)

We will use `httpx`, a modern library that replaces `requests` for asynchrony.

#### 📝 Guided Code: `main.py`

```python
import asyncio
import httpx
import logging
import os
from dotenv import load_dotenv
from functools import wraps
import time

# --- LOGGING CONFIG ---
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')
logger = logging.getLogger(__name__)

# --- TIMING DECORATOR ---
def chrono(func):
    @wraps(func)
    async def wrapper(*args, **kwargs):
        start = time.perf_counter()
        res = await func(*args, **kwargs)
        end = time.perf_counter()
        logger.info(f"⏱️ {func.__name__} took {end - start:.2f}s")
        return res
    return wrapper

# --- SCRAPING LOGIC ---
async def fetch_post(client, post_id):
    url = f"{os.getenv('BASE_URL')}/{post_id}"
    try:
        response = await client.get(url)
        response.raise_for_status()
        data = response.json()
        logger.info(f"✅ Post {post_id} fetched: {data['title'][:20]}...")
        return data
    except Exception as e:
        logger.error(f"❌ Error on post {post_id}: {e}")
        return None

@chrono
async def main():
    load_dotenv()
    ids = range(1, 11) # We fetch the first 10 posts
    
    async with httpx.AsyncClient() as client:
        tasks = [fetch_post(client, i) for i in ids]
        results = await asyncio.gather(*tasks)
    
    valid_results = [r for r in results if r is not None]
    print(f"\n🚀 Total fetched: {len(valid_results)} / {len(ids)}")

if __name__ == "__main__":
    asyncio.run(main())
```

---

## 🧠 Deep Dive: Session vs Isolated Requests (30 min)

> [!IMPORTANT]
> **Why `httpx.AsyncClient()`?**  
> Using a client within an `async with` block allows reusing TCP connections (Keep-Alive). If you created a new client for each request, your program would be much slower and could be banned by the server.

---

## 🧪 EXTRA CHALLENGES (For experts)

### Challenge 1: Rate Limiting
Modify the code to use an `asyncio.Semaphore`. This allows not launching 1000 requests all at once, but for example only 5 at a time.

### Challenge 2: Saving to File
Add a function that saves the results into a `data.json` file at the end of the execution.

---

## ⏳ Month 3 Conclusion

You now have the power of asynchrony in your hands. This skill is what differentiates a junior developer from one capable of managing high-performance systems.

  * **Review:** What are the advantages of `httpx` over `requests`? 
  * **Next Month:** We will use all this knowledge to create real APIs with **FastAPI**!
