# MOIS_3_ASYNCHRONE_OUTILLAGE/SEMAINE_4_Scraper_Projet.md : SEMAINE 4 : Projet – Scraper Web Asynchrone

## 🎯 Objectif du Projet Final
Construire un scraper capable de récupérer des informations sur plusieurs pages web en parallèle, avec gestion des erreurs, logging et configuration par environnement.

---

## 🏗️ Architecture du Projet

Le projet sera structuré ainsi :
```bash
Projet_Scraper/
├── .env                # Clés et configuration
├── .gitignore          # Exclusion du .env
├── app.log             # Historique des opérations
├── main.py             # Cœur du programme
└── requirements.txt    # httpx, python-dotenv
```

---

## 🚀 Étape 1 : Configuration (30 min)

**Objectif :** Préparer l'environnement.

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

## 🛠️ Étape 2 : Le Code Asynchrone (1h30)

Nous allons utiliser `httpx`, une bibliothèque moderne qui remplace `requests` pour l'asynchronisme.

#### 📝 Code Guidé : `main.py`

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

# --- DECORATEUR DE TIMING ---
def chrono(func):
    @wraps(func)
    async def wrapper(*args, **kwargs):
        start = time.perf_counter()
        res = await func(*args, **kwargs)
        end = time.perf_counter()
        logger.info(f"⏱️ {func.__name__} a pris {end - start:.2f}s")
        return res
    return wrapper

# --- LOGIQUE DE SCRAPING ---
async def fetch_post(client, post_id):
    url = f"{os.getenv('BASE_URL')}/{post_id}"
    try:
        response = await client.get(url)
        response.raise_for_status()
        data = response.json()
        logger.info(f"✅ Post {post_id} récupéré : {data['title'][:20]}...")
        return data
    except Exception as e:
        logger.error(f"❌ Erreur sur le post {post_id} : {e}")
        return None

@chrono
async def main():
    load_dotenv()
    ids = range(1, 11) # On récupère les 10 premiers posts
    
    async with httpx.AsyncClient() as client:
        tasks = [fetch_post(client, i) for i in ids]
        resultats = await asyncio.gather(*tasks)
    
    valides = [r for r in resultats if r is not None]
    print(f"\n🚀 Total récupéré : {len(valides)} / {len(ids)}")

if __name__ == "__main__":
    asyncio.run(main())
```

---

## 🧠 Deep Dive : Session vs Requêtes isolées (30 min)

> [!IMPORTANT]
> **Pourquoi `httpx.AsyncClient()` ?**  
> Utiliser un client dans un bloc `async with` permet de réutiliser les connexions TCP (Keep-Alive). Si vous créiez un nouveau client pour chaque requête, votre programme serait beaucoup plus lent et pourrait être banni par le serveur.

---

## 🧪 DÉFIS SUPPLÉMENTAIRES (Pour les experts)

### Défi 1 : Limitation de Débit (Rate Limiting)
Modifiez le code pour utiliser un `asyncio.Semaphore`. Cela permet de ne pas lancer 1000 requêtes d'un coup, mais par exemple seulement 5 à la fois.

### Défi 2 : Sauvegarde en fichier
Ajoutez une fonction qui sauvegarde les résultats dans un fichier `data.json` à la fin de l'exécution.

---

## ⏳ Conclusion du Mois 3

Vous avez maintenant entre les mains le pouvoir de l'asynchronisme. Cette compétence est ce qui différencie un développeur junior d'un développeur capable de gérer des systèmes à haute performance.

  * **Revue :** Quels sont les avantages de `httpx` sur `requests` ? 
  * **Prochain Mois :** Nous allons utiliser toutes ces connaissances pour créer de vraies APIs avec **FastAPI** !
