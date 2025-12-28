# 🛠️ MOIS_1_FONDATIONS/SEMAINE_4_IO_Robustesse_Projet.md : SEMAINE 4 : I/O, Robustesse et Projet Final

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **I/O** | Lire et écrire des données dans des fichiers avec gestion sécurisée. | Maîtrise de `with open()`, `pathlib`. |
| **Robustesse** | Gérer les scénarios d'erreurs réels. | Blocs `try/except/finally` et exceptions personnalisées. |
| **Projet** | Développer un simulateur de bourse intégré. | Synthèse des compétences (POO, I/O, Aléatoire). |

-----

## 1. 📝 Entrées/Sorties : Gestion des Fichiers (60 min)

### Défi 1 : Journalisation des Transactions

**Objectif :** Créer un script qui écrit les transactions dans un fichier.

#### 📝 Code Guidé : `with open()` et `pathlib`

```python
from pathlib import Path

# Utilisation de pathlib (Plus moderne que os.path)
dossier_data = Path("data")
dossier_data.mkdir(exist_ok=True) # Crée le dossier s'il n'existe pas
chemin_fichier = dossier_data / "journal_transactions.txt"

transactions = ["Achat: 100 actions @ 50€", "Vente: 50 actions @ 55€"]

# --- Écriture ---
with open(chemin_fichier, "w", encoding="utf-8") as fichier:
    for t in transactions:
        fichier.write(t + "\n")

print(f"File saved at: {chemin_fichier.absolute()}")
```

> [!IMPORTANT]
> **Deep Dive : Pourquoi le bloc `with` ?**  
> Le mot-clé `with` utilise un **Gestionnaire de Contexte (Context Manager)**. Il garantit que `fichier.close()` est appelé automatiquement, même si une erreur survient pendant l'écriture. Sans cela, vous risquez de corrompre le fichier ou de saturer la mémoire vive.

---

## 2. 🛡️ Robustesse : Gestion des Erreurs (60 min)

### Défi 2 : Gestion d'Erreurs Avancée

**Objectif :** Gérer les fichiers manquants et les entrées invalides avec des messages pros.

#### 📝 Code Guidé : `try/except/finally`

```python
def lire_donnees(nom_fichier):
    try:
        with open(nom_fichier, "r") as f:
            return f.readlines()
    except FileNotFoundError:
        print(f"❌ Erreur : Le fichier '{nom_fichier}' est introuvable.")
    except Exception as e:
        print(f"⚠️ Erreur inattendue : {e}")
    finally:
        print("Opération de lecture terminée.") # S'exécute toujours

entrees = lire_donnees("inexistant.txt")
```

> [!TIP]
> **Pro Tip : Créer ses propres Exceptions**  
> Vous pouvez définir vos propres erreurs pour rendre votre code plus explicite :  
> `class SoldeInsuffisantError(Exception): pass`  
> Cela permet de faire : `raise SoldeInsuffisantError("Vous n'avez pas assez d'argent.")`.

---

## 🎲 Projet Intégrateur : Simulateur de Bourse (60 min)

### Défi 3 : Simulateur de Bourse Intelligent

**Objectif :** Générer des prix, les sauvegarder, et gérer les erreurs de lecture.

#### 📝 Code Guidé : Intégration

```python
import random

def simuler_marche(nb_jours=5):
    historique = []
    for jour in range(1, nb_jours + 1):
        prix = round(random.uniform(50, 150), 2)
        historique.append(f"Jour {jour}: {prix}€")
    
    try:
        with open("bourse.txt", "w") as f:
            f.write("\n".join(historique))
        print("✅ Simulation sauvegardée.")
    except IOError:
        print("❌ Impossible d'écrire sur le disque.")

simuler_marche()
```

> [!WARNING]
> **Piège Courant : Capturer toutes les exceptions**  
> Évitez de faire un `except:` vide sans préciser le type d'erreur. Cela capturera même le `Ctrl+C` (KeyboardInterrupt) et rendra votre programme impossible à arrêter manuellement. Précisez toujours `except ValueError:`, `except FileNotFoundError:`, etc.

---

## 🧪 TP SUPPLÉMENTAIRES (Pour aller plus loin)

### Exercice 1 : Nettoyeur de Fichiers Log
Créez un script qui lit un fichier texte, supprime les lignes vides, et sauvegarde le résultat dans un nouveau fichier `clean_log.txt`.

### Exercice 2 : Système de Sauvegarde Automatique
Utilisez `pathlib` pour lister tous les fichiers `.txt` d'un dossier et les copier dans un dossier `backup/` en ajoutant le préfixe `backup_` à leur nom.

---

## ⏳ Conclusion de Session (15 min)

  * **Revue :** Pourquoi la robustesse est-elle plus importante que la fonctionnalité pure ? (Un code qui crash est inutilisable, peu importe sa puissance).
  * **Fin du Mois 1 :** Félicitations ! Vous maîtrisez les fondations.
  * **Mois 2 :** Préparez-vous à entrer dans le monde de la **Programmation Orientée Objet (POO)**.