
# 🛠️ MOIS\_1\_FONDATIONS/SEMAINE\_1\_Syntaxe\_Types.md : Syntaxe et Types - L'Atelier de Codage

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Setup** | Démarrer un projet Python de zéro (incluant `venv`). | Configuration professionnelle de l'environnement. |
| **Code-First** | Implémenter un script de conversion monétaire ou de temps. | Maîtrise des types (`int`/`float`) et des opérateurs. |
| **Logique** | Écrire une fonction de vérification d'accès sécurisé. | Utilisation idiomatique de `if/elif/else` et des booléens. |

-----

## 1\. 🚀 Démarrage et Environnement (30 min)

### Défi 1 : La Mise en Place du Chantier

**Objectif :** Créer un environnement isolé et respecter la norme de codage dès le départ.

#### Étapes (À exécuter directement)

1.  Ouvrez votre terminal et créez votre dossier de travail : `mkdir MOIS_1_FONDATIONS && cd MOIS_1_FONDATIONS`.
2.  Créez l'environnement virtuel et activez-le : `python -m venv .venv` suivi de `source .venv/bin/activate`.
3.  Créez le premier fichier : `touch SEMAINE_1_Syntaxe_Types.py`.
4.  Dans ce fichier, définissez une variable en respectant **PEP 8 (snake\_case)** :
    ```python
    # Nom de variable conforme (PEP 8) : 
    nom_du_projet = "Simulateur Bourse"
    # Nom de variable NON conforme :
    # NomDuProjet = "..." 
    ```

#### 💡 Théorie Détaillée : Environnement et Standards (PEP 8)

| Concept | Explication Détaillée | Règle du Coder |
| :--- | :--- | :--- |
| **`venv`** | Isole le projet de l'installation Python globale. Garantit que les bibliothèques spécifiques (Mois 4 : FastAPI) n'entrent pas en conflit avec d'autres projets. **Essentiel pour la CI/CD (Mois 6).** | **Obligatoire.** Toujours activer `venv` avant d'installer des dépendances. |
| **PEP 8** | Le guide de style officiel. L'objectif est la **cohérence** entre tous les développeurs Python. Si le code est lisible, il est moins cher à maintenir. | **Priorité absolue.** Utilisez `snake_case` (`variable_longue`) pour les fonctions et variables. **Indentez toujours avec 4 espaces, jamais des tabulations.** |
| **L'Interpréteur** | Python est un langage **interprété**. Le code est exécuté ligne par ligne par un programme (l'interpréteur), ce qui le rend flexible et idéal pour le prototypage rapide. | Simplicité d'exécution : tapez `python nom_fichier.py` pour lancer. |

-----

## 2\. 🧮 Types de Données et Opérateurs (60 min)

### Défi 2 : Le Convertisseur Intelligent

**Objectif :** Écrire un script qui convertit une durée totale en secondes en un format `H:M:S` et qui utilise le formatage **`f-string`**.

#### 📝 Code Guidé : La Solution

Nous devons utiliser les opérateurs **`//` (division entière)** et **`%` (modulo)** pour isoler les minutes et les secondes.

```python
# 1. Donnée d'entrée (à changer par l'utilisateur)
duree_totale_secondes = 9876 

# 2. Calcul des Heures, Minutes, Secondes restantes
heures = duree_totale_secondes // 3600  # Combien de blocs de 3600s ?
secondes_restantes = duree_totale_secondes % 3600

minutes = secondes_restantes // 60      # Combien de blocs de 60s ?
secondes = secondes_restantes % 60

# 3. Affichage professionnel (F-string)
print(f"Durée totale : {heures}h {minutes}m {secondes}s")

# Défi d'extension : afficher le résultat en un seul appel print() en ligne
# print("Résultat : " + str(heures) + "h " + str(minutes) + "m " + str(secondes) + "s") # À éviter !
```

#### 💡 Théorie Détaillée : Typage et Arithmétique Avancée

| Concept | Explication Détaillée | Implication pour le Code |
| :--- | :--- | :--- |
| **Typage Fort et Dynamique** | Python est **dynamique** (le type est vérifié à l'exécution), mais **fort** (vous ne pouvez pas ajouter une `str` et un `int` sans conversion explicite, ex: `"5" + 2` est interdit). | **Clarté :** Utiliser les `f-strings` ou `str()` pour les conversions. |
| **`//` vs. `/`** | **`/`** (division classique) retourne toujours un `float` (ex: `10 / 3` donne `3.333...`). **`//`** (division entière) retourne uniquement la partie entière, sans arrondir (ex: `10 // 3` donne `3`). | **Efficacité :** Utilisez `//` quand seule la quantité entière compte. |
| **`%` (Modulo)** | L'opérateur Modulo retourne le **reste** de la division euclidienne. Crucial pour les vérifications de parité et la conversion d'unités. | **Logique :** C'est l'outil mathématique pour les systèmes cycliques. |
| **`f-strings`** | La méthode la plus moderne et performante de formatage. Elles simplifient la lecture et la mise en forme de données, y compris le contrôle des décimales (`:.2f`). | **Lisibilité :** Toujours privilégier `f-string` sur la concaténation (`+`). |

-----

## 3\. 🚦 Logique Conditionnelle (60 min)

### Défi 3 : Le Garde d'Accès Sécurisé

**Objectif :** Écrire un script qui vérifie si un utilisateur a le droit d'accéder à un système basé sur deux conditions : son statut (Admin ou Utilisateur) et s'il a payé sa licence.

#### 📝 Code Guidé : La Solution `if/elif`

```python
# Variables d'entrée (à manipuler)
statut = "Admin"
licence_active = False
niveau_securite = 4 

# Logique de la porte d'accès
if statut == "Admin" and niveau_securite >= 5:
    # Condition très stricte pour les administrateurs
    print("✅ ACCÈS ADMINISTRATEUR PREMIUM. Bienvenue dans le back-office.")

elif statut == "Admin" and niveau_securite < 5:
    print("⚠️ ACCÈS ADMINISTRATEUR standard. Certains services sont limités.")

elif statut == "Utilisateur" and licence_active:
    # Un utilisateur simple doit avoir une licence active
    print("🔑 ACCÈS UTILISATEUR. Accès aux fonctionnalités de base.")
    
elif not licence_active: 
    # Utilisation de l'opérateur 'not' pour vérifier l'état False
    print("❌ ACCÈS REFUSÉ. Votre licence est inactive.")

else:
    # Cas par défaut si aucune condition ci-dessus n'est remplie
    print("Erreur de statut ou accès non autorisé.")
```

#### 💡 Théorie Détaillée : Logique Booléenne et Conditions

| Concept | Explication Détaillée | Règle du Coder |
| :--- | :--- | :--- |
| **`bool` (True/False)** | La valeur de vérité, la base de toute prise de décision. Notez que Python est sensible à la casse (`True` et `False` avec majuscule). | Les expressions de comparaison (`==`, `>`, `in`) retournent toujours un booléen. |
| **Évaluation en court-circuit** | Python évalue les expressions booléennes de gauche à droite et s'arrête dès que le résultat est connu. Ex: Si `condition_A` est `False` dans `condition_A and condition_B`, Python ne regardera jamais `condition_B`. | **Optimisation :** Placez la condition la plus susceptible d'échouer (et la plus rapide à vérifier) en premier pour les opérations `and`. |
| **`None`** | Représente l'absence de valeur. Il est important de vérifier explicitement si une variable est `None` (`if ma_variable is None:`). | **Vérification de None :** Toujours utiliser `is None` ou `is not None`, jamais `==`. |

### 🧪 TP EXPRESS : Calculateur de Taux de Remise (15 min)

**Consigne :** Créez une variable `montant_total` et une variable `client_fidele` (`True`/`False`).

1.  Si le montant est supérieur à 1000 € **OU** que le client est fidèle, appliquez une remise de 10%.
2.  Sinon, n'appliquez aucune remise.
3.  Affichez le prix final.

<!-- end list -->

```python
# Exemple de départ
montant_total = 1200
client_fidele = False

remise = 0.0

# Complétez ici...
if montant_total > 1000 or client_fidele:
    remise = 0.10
    
prix_final = montant_total * (1 - remise)

print(f"Montant total : {montant_total} €")
print(f"Remise appliquée : {remise * 100}%")
print(f"Prix final : {prix_final:.2f} €")
```

-----

## ⏳ Conclusion de Session (15 min)

  * **Revue de Code :** Correction rapide du TP et discussion sur l'utilisation des parenthèses dans les conditions complexes.
  * **Préparation S2 :** Lecture préparatoire sur les **boucles** (`for`, `while`) et les **fonctions** (`def`). Le codage de la semaine prochaine sera orienté vers l'automatisation.