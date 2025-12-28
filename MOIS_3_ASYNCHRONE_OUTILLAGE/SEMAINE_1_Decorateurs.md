# MOIS_3_ASYNCHRONE_OUTILLAGE/SEMAINE_1_Decorateurs.md : SEMAINE 1 : Décorateurs et Closures

## 🎯 Objectifs de la Session (3h)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Fondations** | Comprendre les fonctions comme "citoyens de premier rang". | Maîtrise des fonctions imbriquées et des **Closures**. |
| **Élégance** | Créer des décorateurs simples pour le logging. | Syntaxe `@decorator`, `wraps`. |
| **Puissance** | Concevoir des décorateurs avec des arguments. | Flexibilité maximale du code. |

---

## 1. Les Closures : L'ADN des Décorateurs (45 min)

Avant de comprendre les décorateurs, il faut comprendre qu'une fonction peut "capturer" son environnement.

### Défi 1 : La Fonction à Mémoire

**Objectif :** Créer une fonction qui se souvient d'une valeur de configuration.

#### 📝 Code Guidé : Closures

```python
def creer_multiplicateur(facteur):
    def multiplier(n):
        return n * facteur
    return multiplier

double = creer_multiplicateur(2)
triple = creer_multiplicateur(3)

print(double(10)) # 20
print(triple(10)) # 30
```

> [!IMPORTANT]
> **Deep Dive : Qu'est-ce qu'une Closure ?**  
> C'est une fonction qui "garde en vie" les variables de sa fonction parente, même après que la fonction parente a fini de s'exécuter. Python stocke cela dans un attribut spécial : `__closure__`.

---

## 2. Les Décorateurs : Modifier sans Toucher (1h15)

Un décorateur est une fonction qui prend une autre fonction et la "décore" avec un nouveau comportement.

### Défi 2 : Le Chronomètre de Fonctions

**Objectif :** Mesurer automatiquement le temps d'exécution d'une fonction.

#### 📝 Code Guidé : `@decorator`

```python
import time
from functools import wraps

def chronometre(fonction):
    @wraps(fonction) # <-- Crucial pour garder les métadonnées de la fonction originale
    def wrapper(*args, **kwargs):
        debut = time.perf_counter()
        resultat = fonction(*args, **kwargs)
        fin = time.perf_counter()
        print(f"⏱️ execution de {fonction.__name__} : {fin - debut:.4f}s")
        return resultat
    return wrapper

@chronometre
def telecharger_donnees():
    time.sleep(1.5)
    print("Données reçues.")

telecharger_donnees()
```

> [!TIP]
> **Pro Tip : L'utilité de `functools.wraps`**  
> Sans `@wraps`, la fonction décorée perdrait son nom et sa documentation (`telecharger_donnees.__name__` deviendrait "wrapper"). Utilisez-le systématiquement.

---

## 3. Décorateurs avec Arguments (1h)

Parfois, on veut passer des options à notre décorateur lui-même.

### Défi 3 : Le Limiteur de Tentatives

**Objectif :** Créer un décorateur qui limite le nombre d'exécutions d'une fonction.

#### 📝 Code Guidé : Triple imbrication

```python
def limiter_tentatives(max_essais):
    def decorateur(fonction):
        essais = 0
        @wraps(fonction)
        def wrapper(*args, **kwargs):
            nonlocal essais # Permet de modifier la variable de la closure
            if essais < max_essais:
                essais += 1
                return fonction(*args, **kwargs)
            else:
                print(f"❌ Erreur : {fonction.__name__} a atteint sa limite.")
        return wrapper
    return decorateur

@limiter_tentatives(max_essais=3)
def envoyer_email():
    print("Email envoyé !")

envoyer_email() # OK
envoyer_email() # OK
envoyer_email() # OK
envoyer_email() # BLOCAGE
```

---

## 🧪 TP SUPPLÉMENTAIRES (Pour aller plus loin)

### Exercice 1 : Logger de Sécurité
Créez un décorateur `@logger` qui enregistre dans un fichier `secu.log` l'heure et le nom de chaque fonction appelée.

### Exercice 2 : Cache de Résultats (Memoization)
Créez un décorateur qui stocke le résultat d'une fonction pour un argument donné dans un dictionnaire. Si on appelle la fonction avec le même argument, on retourne la valeur du cache au lieu de recalculer. (Indice : parfait pour la suite de Fibonacci !).

---

## ⏳ Conclusion de Session (15 min)

  * **Revue :** Pourquoi les décorateurs sont-ils partout dans les frameworks (FastAPI, Flask, Pytest) ? (Parce qu'ils permettent une séparation nette entre la logique métier et les outils transverses comme l'auth ou le logging).
  * **Préparation S2 :** Nous allons découvrir comment Python gère l'attente avec l'Asynchronisme (`asyncio`).
