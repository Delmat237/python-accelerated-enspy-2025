# 🛠️ MOIS_1_FONDATIONS/SEMAINE_1_Syntaxe_Types.md : SEMAINE 1 : Syntaxe et Types

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Setup** | Démarrer un projet Python de zéro. | Configuration professionnelle de l'environnement. |
| **Code-First** | Implémenter un script de conversion. | Maîtrise des types (`int`/`float`) et des opérateurs. |
| **Logique** | Écrire une fonction de vérification d'accès. | Utilisation de `if/elif/else` et des booléens. |

-----

## 1. 🚀 Démarrage et Environnement (30 min)

### Défi 1 : La Mise en Place du Chantier

**Objectif :** Créer un environnement isolé et respecter la norme de codage dès le départ.

#### Étapes (À exécuter directement)

1.  Ouvrez votre terminal et créez votre dossier de travail :
    `mkdir MOIS_1_FONDATIONS && cd MOIS_1_FONDATIONS`
2.  Créez l'environnement virtuel et activez-le :
    `python -m venv .venv` suivi de `source .venv/bin/activate` (Linux/Mac) ou `.venv\Scripts\activate` (Windows).
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
| **`venv`** | Isole le projet de l'installation Python globale. Garantit que les bibliothèques n'entrent pas en conflit. | **Obligatoire.** Toujours activer `venv` avant d'installer des dépendances. |
| **PEP 8** | Le guide de style officiel pour la **cohérence**. Si le code est lisible, il est moins cher à maintenir. | **Priorité absolue.** Utilisez `snake_case`. **Indentez toujours avec 4 espaces.** |
| **L'Interpréteur** | Python est un langage **interprété**. Le code est exécuté ligne par ligne. | tapez `python nom_fichier.py` pour lancer. |

> [!TIP]
> **Pro Tip :** Utilisez des noms de variables descriptifs. Évitez `a`, `b`, `c`. Préférez `age_utilisateur` ou `prix_unitaire`. Votre "vous" du futur vous remerciera lors du débogage !

---

## 2. 🧮 Types de Données et Opérateurs (60 min)

### Défi 2 : Le Convertisseur Intelligent

**Objectif :** Écrire un script qui convertit une durée totale en secondes en format `H:M:S` avec **`f-string`**.

#### 📝 Code Guidé : La Solution

```python
# 1. Donnée d'entrée
duree_totale_secondes = 9876 

# 2. Calcul des Heures, Minutes, Secondes
heures = duree_totale_secondes // 3600  
secondes_restantes = duree_totale_secondes % 3600

minutes = secondes_restantes // 60      
secondes = secondes_restantes % 60

# 3. Affichage professionnel (F-string)
print(f"Durée totale : {heures}h {minutes}m {secondes}s")
```

#### 💡 Théorie Détaillée : Arithmétique et Typage

| Concept | Explication | Implication |
| :--- | :--- | :--- |
| **Typage Fort** | Python interdit les opérations entre types incompatibles (ex: `"5" + 2`). | Vous devez convertir explicitement : `int("5") + 2`. |
| **Typage Dynamique** | Une variable peut changer de type au cours de l'exécution. | Flexibilité totale, mais attention aux erreurs de logique. |
| **`//` vs. `/`** | **`/`** (division classique) donne toujours un `float`. **`//`** (division entière) donne un `int`. | Crucial pour les indices ou les comptes ronds. |

> [!IMPORTANT]
> **Deep Dive : La Mémoire et `id()`**  
> En Python, tout est objet. Vous pouvez voir l'adresse mémoire d'une variable avec `id(nom_variable)`.  
> `x = 10` -> `id(x)` donnera l'emplacement de l'entier 10. Si vous faites `y = 10`, `id(y)` sera souvent identique car Python optimise les petits entiers (interning).

---

## 3. 🚦 Logique Conditionnelle (60 min)

### Défi 3 : Le Garde d'Accès Sécurisé

**Objectif :** Vérifier les droits d'accès basés sur le statut et la licence.

#### 📝 Code Guidé : La Solution `if/elif`

```python
# Variables d'entrée
statut = "Admin"
licence_active = False
niveau_securite = 4 

# Logique de la porte d'accès
if statut == "Admin" and niveau_securite >= 5:
    print("✅ ACCÈS ADMINISTRATEUR PREMIUM.")
elif statut == "Admin" or niveau_securite == 4:
    print("⚠️ ACCÈS ADMINISTRATEUR standard ou niveau 4.")
elif not licence_active: 
    print("❌ ACCÈS REFUSÉ. Licence inactive.")
else:
    print("Erreur de statut.")
```

> [!WARNING]
> **Piège Courant : L'évaluation en court-circuit**  
> Dans un `and`, si la première condition est `False`, Python n'évalue pas la seconde.  
> Dans un `or`, si la première est `True`, il s'arrête là.  
> *Conséquence :* Placez les conditions les plus "légères" ou les plus probables en premier pour optimiser.

---

## 🧪 TP SUPPLÉMENTAIRES (Pour aller plus loin)

### Exercice 1 : Analyse de Nombre
Demandez un nombre à l'utilisateur (via `input()`). 
1. Vérifiez s'il est pair ou impair (indice : utilisez `% 2`).
2. Vérifiez s'il est positif, négatif ou nul.
3. Affichez un message complet.

### Exercice 2 : Calculateur de IMC (Indice de Masse Corporelle)
1. Créez des variables `poids` (kg) et `taille` (m).
2. Calculez l'IMC : `poids / (taille ** 2)`.
3. Affichez la catégorie selon l'OMS :
   - < 18.5 : Maigreur
   - 18.5 à 25 : Normal
   - > 25 : Surpoids

---

## ⏳ Conclusion de Session (15 min)

  * **Revue de Code :** Pourquoi l'indentation est-elle obligatoire en Python ? (Réponse : Elle définit les blocs de code).
  * **Préparation S2 :** Nous apprendrons à répéter des actions sans copier-coller (Boucles).