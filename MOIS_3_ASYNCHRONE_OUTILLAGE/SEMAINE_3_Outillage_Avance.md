# MOIS_3_ASYNCHRONE_OUTILLAGE/SEMAINE_3_Outillage_Avance.md : SEMAINE 3 : Outillage Avancé et Logging

## 🎯 Objectifs de la Session (3h)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Surveillance** | Remplacer `print()` par le module `logging`. | Niveaux de log, formateurs, gestionnaires. |
| **Sécurité** | Gérer les secrets avec des fichiers `.env`. | Bibliothèque `python-dotenv`. |
| **Robustesse** | Créer un système de gestion d'erreurs global. | Utilisation avancée de `sys.excepthook`. |

---

## 1. Le Logging : Voir ce que fait votre code (1h15)

En production, vous ne pouvez pas voir l'écran de l'utilisateur. Le logging écrit l'histoire de votre programme dans un fichier.

### Défi 1 : Configuration d'un Logger Pro

**Objectif :** Créer un système qui écrit les erreurs dans un fichier et les infos dans la console.

#### 📝 Code Guidé : `logging`

```python
import logging

# 1. Création du logger
logger = logging.getLogger("MonApp")
logger.setLevel(logging.DEBUG)

# 2. Création des handlers (Destinations)
console_handler = logging.StreamHandler()
file_handler = logging.FileHandler("app.log")

# 3. Création d'un format élégant
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
console_handler.setFormatter(formatter)
file_handler.setFormatter(formatter)

# 4. Ajout des handlers au logger
logger.addHandler(console_handler)
logger.addHandler(file_handler)

# Tests
logger.info("L'application a démarré.")
logger.warning("Attention : l'espace disque est faible.")
logger.error("Erreur critique : connexion base de données échouée.")
```

> [!IMPORTANT]
> **Deep Dive : Les Niveaux de Log**  
> - `DEBUG` : Détails techniques pour le développement.
> - `INFO` : Confirmation que tout se passe comme prévu.
> - `WARNING` : Quelque chose d'inattendu, mais l'app tourne encore.
> - `ERROR` : Un problème sérieux, une fonctionnalité a échoué.
> - `CRITICAL` : L'application entière risque de s'arrêter.

---

## 2. Variables d'Environnement : Ne jamais coder de mots de passe (45 min)

### Défi 2 : Sécuriser les accès

**Objectif :** Utiliser `.env` pour stocker une clé API.

#### Étapes :
1. Installez : `pip install python-dotenv`
2. Créez un fichier `.env` : `API_KEY=votre_cle_secrete_123`

#### 📝 Code Guidé : `dotenv`

```python
import os
from dotenv import load_dotenv

load_dotenv() # Charge le fichier .env en mémoire

api_key = os.getenv("API_KEY")

if api_key:
    print(f"✅ Clé API chargée : {api_key[:4]}****")
else:
    print("❌ Erreur : Clé API introuvable dans le .env")
```

> [!TIP]
> **Pro Tip : `.gitignore`**  
> N'oubliez **jamais** d'ajouter `.env` à votre fichier `.gitignore` pour ne pas envoyer vos accès secrets sur GitHub !

---

## 3. Gestion d'Erreurs Globale (1h)

En plus du `try/except`, on peut capturer toutes les erreurs qui auraient été oubliées.

#### 📝 Code Guidé : `excepthook`

```python
import sys

def capteur_erreurs_global(type_err, valeur_err, trace_err):
    logger.critical(f"UNCAUGHT EXCEPTION: {valeur_err}", exc_info=(type_err, valeur_err, trace_err))

sys.excepthook = capteur_erreurs_global

# Teste un crash
1 / 0
```

---

## 🧪 TP SUPPLÉMENTAIRES (Pour aller plus loin)

### Exercice 1 : Rotation de Logs
Utilisez `RotatingFileHandler` pour que votre fichier de log ne dépasse jamais 1 Mo, en gardant les 5 derniers fichiers.

### Exercice 2 : Validateur de Config
Créez un script qui vérifie au démarrage si toutes les variables nécessaires (DATABASE_URL, SECRET_KEY) sont présentes dans le `.env` et refuse de démarrer s'il en manque une.

---

## ⏳ Conclusion de Session (15 min)

  * **Revue :** Pourquoi `print()` est banni en milieu professionnel ? (Impossible à filtrer, n'enregistre rien durablement, ralentit l'affichage).
  * **Préparation S4 :** Le Grand Projet ! Nous allons construire un Scraper Web asynchrone ultra-puissant.
