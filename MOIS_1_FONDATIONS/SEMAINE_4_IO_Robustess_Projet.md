# 🛠️ MOIS_1_FONDATIONS/SEMAINE_4_IO_Robustesse_Projet.md : I/O, Robustesse et Projet Final

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **I/O** | Lire et écrire des données dans des fichiers texte avec gestion sécurisée. | Maîtrise de `with open()`, lecture/écriture de fichiers. |
| **Robustesse** | Gérer les erreurs potentielles dans un script avec des blocs `try/except`. | Utilisation de la gestion d'exceptions pour une exécution stable. |
| **Projet** | Développer un simulateur de bourse simple intégrant I/O, robustesse et aléatoire. | Synthèse des compétences du mois 1 avec le module `random`. |

-----

## 1\. 📝 Entrées/Sorties : Gestion des Fichiers (60 min)

Les fichiers permettent de persister les données entre les exécutions d'un programme.

### Défi 1 : Journalisation des Transactions

**Objectif :** Créer un script qui écrit les transactions dans un fichier et les lit pour un rapport.

#### 📝 Code Guidé : `with open()`

```python
# --- Écriture dans un fichier ---
transactions = ["Achat: 100 actions @ 50€", "Vente: 50 actions @ 55€"]

with open("journal_transactions.txt", "w") as fichier:
    for transaction in transactions:
        fichier.write(transaction + "\n")

print("Transactions enregistrées avec succès.")

# --- Lecture du fichier ---
with open("journal_transactions.txt", "r") as fichier:
    contenu = fichier.readlines()
    print("Rapport des Transactions:")
    for ligne in contenu:
        print(f"- {ligne.strip()}")
```

#### 💡 Théorie Brève : `with` et Modes de Fichier

  * **`with`:** Assure que le fichier est correctement fermé après utilisation, évitant les fuites de ressources.
  * **Modes:** `"w"` (écriture, écrasement), `"a"` (ajout), `"r"` (lecture, par défaut).

#### Défi d'Extension : Ajouter une nouvelle transaction en mode "a" sans écraser les données existantes.

-----

## 2\. 🛡️ Robustesse : Gestion des Erreurs (60 min)

Les erreurs sont inévitables. La gestion avec `try/except` rend les scripts fiables.

### Défi 2 : Conversion de Données avec Gestion d'Erreurs

**Objectif :** Convertir une entrée utilisateur en nombre, avec gestion des cas d'erreur.

#### 📝 Code Guidé : `try/except`

```python
def convertir_en_nombre(valeur):
    try:
        nombre = float(valeur)
        return nombre
    except ValueError:
        print(f"Erreur : '{valeur}' n'est pas un nombre valide.")
        return None

# Test avec des entrées
entrees = ["123.45", "abc", "50.0"]

for entree in entrees:
    resultat = convertir_en_nombre(entree)
    if resultat is not None:
        print(f"Conversion réussie : {resultat}")
```

#### 💡 Théorie Brève : Exceptions

  * **`try/except`:** Capture les erreurs (ex: `ValueError`, `FileNotFoundError`) pour éviter les crashs.
  * **Bonnes Pratiques:** Toujours gérer les cas d'échec avec un message clair.

#### Défi d'Extension : Ajouter une gestion pour `ZeroDivisionError` si une division est tentée.

-----

## 3\. 🎲 Projet Intégrateur : Simulateur de Bourse (60 min)

### Défi 3 : Simulateur de Bourse avec `random`

**Objectif :** Développer un simulateur qui génère aléatoirement des prix d'actions, les enregistre, et calcule un gain net avec gestion d'erreurs.

#### 📝 Code Guidé : Intégration I/O, Robustesse et `random`

```python
import random

# Fonction pour générer un prix aléatoire
def generer_prix_action():
    return round(random.uniform(10.0, 100.0), 2)

# Simulation
portefeuille = {}
nb_jours = 5

try:
    with open("historique_bourse.txt", "w") as fichier:
        for jour in range(1, nb_jours + 1):
            action = f"ACT{jour}"
            prix = generer_prix_action()
            portefeuille[action] = prix
            fichier.write(f"Jour {jour}: {action} @ {prix}€\n")

    # Calcul du gain net (simulé avec une vente aléatoire)
    gain_net = 0
    with open("historique_bourse.txt", "r") as fichier:
        for ligne in fichier:
            parts = ligne.strip().split(" @ ")
            if len(parts) == 2:
                prix_achat = float(parts[1].replace("€", ""))
                prix_vente = generer_prix_action()
                gain = prix_vente - prix_achat
                gain_net += gain
                print(f"{parts[0]}: Achat={prix_achat}€, Vente={prix_vente}€, Gain={gain:.2f}€")

    print(f"Gain net total: {gain_net:.2f}€")

except (ValueError, FileNotFoundError) as e:
    print(f"Erreur lors de la simulation : {e}")
```

#### 💡 Théorie Brève : `random`

  * **`random.uniform(a, b)`:** Génère un nombre flottant aléatoire entre `a` et `b`.
  * **Utilité:** Simuler des données imprévisibles comme les prix boursiers.

#### 🧪 TP EXPRESS : Amélioration (15 min)

**Consigne :**
1. Ajoutez une vérification pour s'assurer que le prix généré est supérieur à 20€.
2. Enregistrez uniquement les gains positifs dans un fichier `gains_positifs.txt`.

```python
# Votre code ici...
```

-----

## ⏳ Conclusion de Session (15 min)

  * **Revue de Code:** Analyse du projet, focus sur la gestion d'erreurs et l'utilisation de `random`.
  * **Synthèse Mois 1:** Vous avez maîtrisé la syntaxe, les boucles, les fonctions, les structures de données, et maintenant la robustesse et les I/O. Le fichier `simulateur.py` dans `TP_Simulateur_Bourse/` est votre livrable.
  * **Préparation Mois 2:** Explorez les bases de la POO dans `MOIS_2_POO_AVANCEE/SEMAINE_1_Classes_Encapsulation.md`.

Ce cours privilégie la pratique pour consolider les compétences du mois 1 avec un projet concret.

---

<xaiArtifact artifact_id="b8e0b986-00bd-4adb-82e4-866017836e3d" artifact_version_id="05dbcca2-f681-4f64-bc07-42f33550aa4a" title="MOIS_1_FONDATIONS/SEMAINE_4_IO_Robustesse_Projet.md" contentType="text/markdown">

# 🛠️ MOIS_1_FONDATIONS/SEMAINE_4_IO_Robustesse_Projet.md : I/O, Robustesse et Projet Final

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **I/O** | Lire et écrire des données dans des fichiers texte avec gestion sécurisée. | Maîtrise de `with open()`, lecture/écriture de fichiers. |
| **Robustesse** | Gérer les erreurs potentielles dans un script avec des blocs `try/except`. | Utilisation de la gestion d'exceptions pour une exécution stable. |
| **Projet** | Développer un simulateur de bourse simple intégrant I/O, robustesse et aléatoire. | Synthèse des compétences du mois 1 avec le module `random`. |

-----

## 1\. 📝 Entrées/Sorties : Gestion des Fichiers (60 min)

Les fichiers permettent de persister les données entre les exécutions d'un programme.

### Défi 1 : Journalisation des Transactions

**Objectif :** Créer un script qui écrit les transactions dans un fichier et les lit pour un rapport.

#### 📝 Code Guidé : `with open()`

```python
# --- Écriture dans un fichier ---
transactions = ["Achat: 100 actions @ 50€", "Vente: 50 actions @ 55€"]

with open("journal_transactions.txt", "w") as fichier:
    for transaction in transactions:
        fichier.write(transaction + "\n")

print("Transactions enregistrées avec succès.")

# --- Lecture du fichier ---
with open("journal_transactions.txt", "r") as fichier:
    contenu = fichier.readlines()
    print("Rapport des Transactions:")
    for ligne in contenu:
        print(f"- {ligne.strip()}")
```

#### 💡 Théorie Brève : `with` et Modes de Fichier

  * **`with`:** Assure que le fichier est correctement fermé après utilisation, évitant les fuites de ressources.
  * **Modes:** `"w"` (écriture, écrasement), `"a"` (ajout), `"r"` (lecture, par défaut).

#### Défi d'Extension : Ajouter une nouvelle transaction en mode "a" sans écraser les données existantes.

-----

## 2\. 🛡️ Robustesse : Gestion des Erreurs (60 min)

Les erreurs sont inévitables. La gestion avec `try/except` rend les scripts fiables.

### Défi 2 : Conversion de Données avec Gestion d'Erreurs

**Objectif :** Convertir une entrée utilisateur en nombre, avec gestion des cas d'erreur.

#### 📝 Code Guidé : `try/except`

```python
def convertir_en_nombre(valeur):
    try:
        nombre = float(valeur)
        return nombre
    except ValueError:
        print(f"Erreur : '{valeur}' n'est pas un nombre valide.")
        return None

# Test avec des entrées
entrees = ["123.45", "abc", "50.0"]

for entree in entrees:
    resultat = convertir_en_nombre(entree)
    if resultat is not None:
        print(f"Conversion réussie : {resultat}")
```

#### 💡 Théorie Brève : Exceptions

  * **`try/except`:** Capture les erreurs (ex: `ValueError`, `FileNotFoundError`) pour éviter les crashs.
  * **Bonnes Pratiques:** Toujours gérer les cas d'échec avec un message clair.

#### Défi d'Extension : Ajouter une gestion pour `ZeroDivisionError` si une division est tentée.

-----

## 3\. 🎲 Projet Intégrateur : Simulateur de Bourse (60 min)

### Défi 3 : Simulateur de Bourse avec `random`

**Objectif :** Développer un simulateur qui génère aléatoirement des prix d'actions, les enregistre, et calcule un gain net avec gestion d'erreurs.

#### 📝 Code Guidé : Intégration I/O, Robustesse et `random`

```python
import random

# Fonction pour générer un prix aléatoire
def generer_prix_action():
    return round(random.uniform(10.0, 100.0), 2)

# Simulation
portefeuille = {}
nb_jours = 5

try:
    with open("historique_bourse.txt", "w") as fichier:
        for jour in range(1, nb_jours + 1):
            action = f"ACT{jour}"
            prix = generer_prix_action()
            portefeuille[action] = prix
            fichier.write(f"Jour {jour}: {action} @ {prix}€\n")

    # Calcul du gain net (simulé avec une vente aléatoire)
    gain_net = 0
    with open("historique_bourse.txt", "r") as fichier:
        for ligne in fichier:
            parts = ligne.strip().split(" @ ")
            if len(parts) == 2:
                prix_achat = float(parts[1].replace("€", ""))
                prix_vente = generer_prix_action()
                gain = prix_vente - prix_achat
                gain_net += gain
                print(f"{parts[0]}: Achat={prix_achat}€, Vente={prix_vente}€, Gain={gain:.2f}€")

    print(f"Gain net total: {gain_net:.2f}€")

except (ValueError, FileNotFoundError) as e:
    print(f"Erreur lors de la simulation : {e}")
```

#### 💡 Théorie Brève : `random`

  * **`random.uniform(a, b)`:** Génère un nombre flottant aléatoire entre `a` et `b`.
  * **Utilité:** Simuler des données imprévisibles comme les prix boursiers.

#### 🧪 TP EXPRESS : Amélioration (15 min)

**Consigne :**
1. Ajoutez une vérification pour s'assurer que le prix généré est supérieur à 20€.
2. Enregistrez uniquement les gains positifs dans un fichier `gains_positifs.txt`.

```python
# Votre code ici...
```

-----

## ⏳ Conclusion de Session (15 min)

  * **Revue de Code:** Analyse du projet, focus sur la gestion d'erreurs et l'utilisation de `random`.
  * **Synthèse Mois 1:** Vous avez maîtrisé la syntaxe, les boucles, les fonctions, les structures de données, et maintenant la robustesse et les I/O. Le fichier `simulateur.py` dans `TP_Simulateur_Bourse/` est votre livrable.
  * **Préparation Mois 2:** Explorez les bases de la POO dans `MOIS_2_POO_AVANCEE/SEMAINE_1_Classes_Encapsulation.md`.

Ce cours privilégie la pratique pour consolider les compétences du mois 1 avec un projet concret.

</xaiArtifact>

Ce cours est placé sous `MOIS_1_FONDATIONS/SEMAINE_4_IO_Robustesse_Projet.md` et intègre les trois axes demandés : I/O avec `with open()`, robustesse avec `try/except`, et un projet utilisant `random`. Il inclut des défis pratiques, des explications théoriques, et un TP pour renforcer l'apprentissage. Le livrable est aligné avec `TP_Simulateur_Bourse/simulateur.py` comme spécifié dans votre structure. Si vous souhaitez des ajustements ou des ajouts (ex: plus de détails sur le TP), faites-le-moi savoir !

# 🛠️ MOIS_1_FONDATIONS/SEMAINE_4_IO_Robustesse_Projet.md : I/O, Robustesse et Projet Final

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **I/O** | Lire et écrire des données dans des fichiers texte avec gestion sécurisée. | Maîtrise de `with open()`, lecture/écriture de fichiers. |
| **Robustesse** | Gérer les erreurs potentielles dans un script avec des blocs `try/except`. | Utilisation de la gestion d'exceptions pour une exécution stable. |
| **Projet** | Développer un simulateur de bourse simple intégrant I/O, robustesse et aléatoire. | Synthèse des compétences du mois 1 avec le module `random`. |

-----

## 1\. 📝 Entrées/Sorties : Gestion des Fichiers (60 min)

Les fichiers permettent de persister les données entre les exécutions d'un programme.

### Défi 1 : Journalisation des Transactions

**Objectif :** Créer un script qui écrit les transactions dans un fichier et les lit pour un rapport.

#### 📝 Code Guidé : `with open()`

```python
# --- Écriture dans un fichier ---
transactions = ["Achat: 100 actions @ 50€", "Vente: 50 actions @ 55€"]

with open("journal_transactions.txt", "w") as fichier:
    for transaction in transactions:
        fichier.write(transaction + "\n")

print("Transactions enregistrées avec succès.")

# --- Lecture du fichier ---
with open("journal_transactions.txt", "r") as fichier:
    contenu = fichier.readlines()
    print("Rapport des Transactions:")
    for ligne in contenu:
        print(f"- {ligne.strip()}")
```

#### 💡 Théorie Brève : `with` et Modes de Fichier

  * **`with`:** Assure que le fichier est correctement fermé après utilisation, évitant les fuites de ressources.
  * **Modes:** `"w"` (écriture, écrasement), `"a"` (ajout), `"r"` (lecture, par défaut).

#### Défi d'Extension : Ajouter une nouvelle transaction en mode "a" sans écraser les données existantes.

-----

## 2\. 🛡️ Robustesse : Gestion des Erreurs (60 min)

Les erreurs sont inévitables. La gestion avec `try/except` rend les scripts fiables.

### Défi 2 : Conversion de Données avec Gestion d'Erreurs

**Objectif :** Convertir une entrée utilisateur en nombre, avec gestion des cas d'erreur.

#### 📝 Code Guidé : `try/except`

```python
def convertir_en_nombre(valeur):
    try:
        nombre = float(valeur)
        return nombre
    except ValueError:
        print(f"Erreur : '{valeur}' n'est pas un nombre valide.")
        return None

# Test avec des entrées
entrees = ["123.45", "abc", "50.0"]

for entree in entrees:
    resultat = convertir_en_nombre(entree)
    if resultat is not None:
        print(f"Conversion réussie : {resultat}")
```

#### 💡 Théorie Brève : Exceptions

  * **`try/except`:** Capture les erreurs (ex: `ValueError`, `FileNotFoundError`) pour éviter les crashs.
  * **Bonnes Pratiques:** Toujours gérer les cas d'échec avec un message clair.

#### Défi d'Extension : Ajouter une gestion pour `ZeroDivisionError` si une division est tentée.

-----

## 3\. 🎲 Projet Intégrateur : Simulateur de Bourse (60 min)

### Défi 3 : Simulateur de Bourse avec `random`

**Objectif :** Développer un simulateur qui génère aléatoirement des prix d'actions, les enregistre, et calcule un gain net avec gestion d'erreurs.

#### 📝 Code Guidé : Intégration I/O, Robustesse et `random`

```python
import random

# Fonction pour générer un prix aléatoire
def generer_prix_action():
    return round(random.uniform(10.0, 100.0), 2)

# Simulation
portefeuille = {}
nb_jours = 5

try:
    with open("historique_bourse.txt", "w") as fichier:
        for jour in range(1, nb_jours + 1):
            action = f"ACT{jour}"
            prix = generer_prix_action()
            portefeuille[action] = prix
            fichier.write(f"Jour {jour}: {action} @ {prix}€\n")

    # Calcul du gain net (simulé avec une vente aléatoire)
    gain_net = 0
    with open("historique_bourse.txt", "r") as fichier:
        for ligne in fichier:
            parts = ligne.strip().split(" @ ")
            if len(parts) == 2:
                prix_achat = float(parts[1].replace("€", ""))
                prix_vente = generer_prix_action()
                gain = prix_vente - prix_achat
                gain_net += gain
                print(f"{parts[0]}: Achat={prix_achat}€, Vente={prix_vente}€, Gain={gain:.2f}€")

    print(f"Gain net total: {gain_net:.2f}€")

except (ValueError, FileNotFoundError) as e:
    print(f"Erreur lors de la simulation : {e}")
```

#### 💡 Théorie Brève : `random`

  * **`random.uniform(a, b)`:** Génère un nombre flottant aléatoire entre `a` et `b`.
  * **Utilité:** Simuler des données imprévisibles comme les prix boursiers.

#### 🧪 TP EXPRESS : Amélioration (15 min)

**Consigne :**
1. Ajoutez une vérification pour s'assurer que le prix généré est supérieur à 20€.
2. Enregistrez uniquement les gains positifs dans un fichier `gains_positifs.txt`.

```python
# Votre code ici...
```

-----

## ⏳ Conclusion de Session (15 min)

  * **Revue de Code:** Analyse du projet, focus sur la gestion d'erreurs et l'utilisation de `random`.
  * **Synthèse Mois 1:** Vous avez maîtrisé la syntaxe, les boucles, les fonctions, les structures de données, et maintenant la robustesse et les I/O. Le fichier `simulateur.py` dans `TP_Simulateur_Bourse/` est votre livrable.
  * **Préparation Mois 2:** Explorez les bases de la POO dans `MOIS_2_POO_AVANCEE/SEMAINE_1_Classes_Encapsulation.md`.

Ce cours privilégie la pratique pour consolider les compétences du mois 1 avec un projet concret.