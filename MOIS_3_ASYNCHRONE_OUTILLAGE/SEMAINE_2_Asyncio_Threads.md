# MOIS_3_ASYNCHRONE_OUTILLAGE/SEMAINE_2_Asyncio_Threads.md : SEMAINE 2 : Asyncio et Multi-threading

## 🎯 Objectifs de la Session (3h)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Concept** | Comprendre la différence entre synchrone et asynchrone. | Analogie du restaurant, boucle d'événements. |
| **Asynchronisme** | Utiliser `async`, `await` et `gather`. | Maîtrise de la bibliothèque `asyncio`. |
| **Parallélisme** | Savoir quand utiliser le Multi-threading. | Utilisation de `ThreadPoolExecutor`. |

---

## 1. Analogie : Le Restaurant de l'Asynchronisme (30 min)

Imaginez un serveur dans un restaurant :
- **Synchrone :** Le serveur prend une commande, va en cuisine, et attend que le plat soit prêt avant de servir le client et de passer au suivant. (Gaspillage de temps !)
- **Asynchrone :** Le serveur prend la commande, la donne en cuisine, et va prendre une autre commande en attendant que le premier plat soit prêt. (Efficacité maximale !)

---

## 2. Asyncio : La Magie de l'Attente (1h15)

`asyncio` est le cœur de la programmation asynchrone en Python.

### Défi 1 : Le Simulacre de Requêtes Web

**Objectif :** Télécharger plusieurs "pages" simultanément sans bloquer le programme.

#### 📝 Code Guidé : `async/await`

```python
import asyncio
import time

async def simuler_requete(nom, delai):
    print(f"🚀 Début de la requête {nom}...")
    await asyncio.sleep(delai) # <-- On attend sans bloquer
    print(f"✅ Requête {nom} terminée après {delai}s")
    return f"Résultat {nom}"

async def main():
    debut = time.perf_counter()
    
    # Lancement SIMULTANÉ
    resultats = await asyncio.gather(
        simuler_requete("A", 2),
        simuler_requete("B", 1),
        simuler_requete("C", 1.5)
    )
    
    fin = time.perf_counter()
    print(f"\nTemps total : {fin - debut:.2f}s")
    print(f"Résultats : {resultats}")

if __name__ == "__main__":
    asyncio.run(main())
```

> [!IMPORTANT]
> **Deep Dive : La Boucle d'Événements (Event Loop)**  
> Python utilise un seul fil d'exécution (thread) mais passe d'une tâche à l'autre dès qu'un `await` est rencontré. C'est l'Event Loop qui gère ce planning ultra-rapide.

---

## 3. Multi-threading : Quand Asyncio ne suffit plus (1h)

L'asynchronisme est parfait pour l'**I/O (réseau, fichiers)**. Mais pour des calculs lourds (CPU), on a besoin du Multi-threading ou du Multi-processing.

### Défi 2 : Traitement de Fichiers en Parallèle

#### 📝 Code Guidé : `ThreadPoolExecutor`

```python
from concurrent.futures import ThreadPoolExecutor
import time

def tache_lourde(n):
    print(f"🔨 Calcul pour {n} commencé...")
    time.sleep(1) # Simule un calcul
    return n * n

with ThreadPoolExecutor(max_workers=3) as executeur:
    nombres = [1, 2, 3, 4, 5]
    resultats = list(executeur.map(tache_lourde, nombres))

print(f"Résultats finaux : {resultats}")
```

> [!WARNING]
> **Piège Courant : Le GIL (Global Interpreter Lock)**  
> En Python, deux threads ne peuvent pas exécuter du code Python en même temps sur le même CPU. Le multi-threading est donc utile pour l'attente (I/O) mais pas pour accélérer les calculs mathématiques purs (utilisez `multiprocessing` pour cela).

---

## 🧪 TP SUPPLÉMENTAIRES (Pour aller plus loin)

### Exercice 1 : Scanner de Ports Asynchrone
Écrivez un script `asyncio` qui tente de se connecter à une liste de ports (80, 443, 22) sur un serveur de test pour voir s'ils sont ouverts.

### Exercice 2 : Comparaison de Vitesse
Créez un script qui télécharge 5 fois la même URL (utilisez un délai fictif) :
1. De façon classique (synchrone).
2. Avec `asyncio.gather`.
Affichez la différence de temps.

---

## ⏳ Conclusion de Session (15 min)

  * **Revue :** Quand utiliser `asyncio` ? (Quand on a beaucoup d'attente réseau/disque).
  * **Préparation S3 :** Nous verrons comment surveiller nos programmes avec le Logging professionnel.
