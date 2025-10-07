Absolument. En se basant sur la philosophie **Code-First** inspirée des meilleurs cours intensifs, la Semaine 3 se concentre sur l'outil le plus puissant de Python : la manipulation efficace des **structures de données** et l'**optimisation** grâce aux compréhensions.

Voici le contenu de la **Semaine 3** du **Mois 1**, structuré pour une session pratique de 2h à 2h30.

-----

# 🛠️ MOIS 1 / SEMAINE 3 : Structures de Données et Efficacité

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Sécurité/Efficacité** | Gérer un inventaire modifiable (`list`) et des identifiants non modifiables (`tuple`). | Maîtrise de la **mutabilité** et des méthodes de séquences. |
| **Modélisation** | Représenter un objet complexe (ex: un produit ou un profil utilisateur) avec des paires clé-valeur. | Utilisation professionnelle des **dictionnaires** (`dict`). |
| **Optimisation** | Réduire 5 à 10 lignes de code en une seule ligne élégante et performante. | Maîtrise des **Compréhensions de Liste et de Dictionnaire**. |

-----

## 1\. 📦 Séquences : Listes et Tuples (45 min)

### Défi 1 : Gestion d'Inventaire et de Coordonnées

**Objectif :** Utiliser la structure de données appropriée pour gérer un inventaire qui change (Liste) et des coordonnées GPS qui ne doivent pas être altérées (Tuple).

#### 📝 Code Guidé : Mutabilité vs. Immutabilité

```python
# --- Partie 1 : Inventaire Modifiable (Listes) ---
inventaire_produits = ["Rotor X1", "Capteur Z", "Vanne A"]

# Action 1: Ajouter un nouvel élément à la fin
inventaire_produits.append("Filtre H9")
print(f"1. Après ajout: {inventaire_produits}")

# Action 2: Supprimer le Capteur Z
inventaire_produits.remove("Capteur Z")
print(f"2. Après suppression: {inventaire_produits}")

# Action 3: Lister uniquement les 2 derniers produits (Slicing)
derniers_produits = inventaire_produits[-2:]
print(f"3. Les deux derniers: {derniers_produits}")

print("-" * 20)

# --- Partie 2 : Coordonnées (Tuples Immutables) ---
# Un tuple est plus léger et plus rapide pour des données fixes
coordonnees_usine = (48.8584, 2.2945)

# Tenter de modifier le tuple (DOIT lever une erreur)
try:
    coordonnees_usine[0] = 49.0
except TypeError as e:
    print(f"4. ERREUR attendue: {e}")

# Bonne pratique : Déstructuration du tuple
lat, lon = coordonnees_usine
print(f"5. Latitude déstructurée: {lat}")
```

#### 💡 Théorie Brève : Le "Pourquoi" du Choix

  * **Listes (Mutables) :** Flexibilité. Idéales pour les données dynamiques (inventaires, journaux, listes de résultats).
  * **Tuples (Immutables) :** Sécurité et rapidité. Idéales pour les données constantes (coordonnées, clés composites, paramètres de configuration).

-----

## 2\. 🗺️ Mapping : Dictionnaires (60 min)

### Défi 2 : Modélisation d'un Rapport d'Incident

**Objectif :** Modéliser un objet complexe (un rapport d'incident) en utilisant un dictionnaire, et apprendre à y accéder de manière sûre, y compris les données imbriquées.

#### 📝 Code Guidé : Accès Sécurisé et Itération

```python
# Modélisation d'un rapport d'incident (clé:valeur)
rapport_incident = {
    "reference_id": "INC-2025-452",
    "gravite": "Haute",
    "date": "2025-01-20",
    "statut": "Ouvert",
    "details_auteur": {
        "nom": "Durand",
        "service": "Maintenance",
        "contact": "durand@enspy.cm"
    },
    "actions_necessaires": ["Isoler le système", "Lancer un diagnostic"]
}

# 1. Accès sécurisé : Utiliser .get() pour éviter le plantage
service_contact = rapport_incident.get("details_auteur", {}).get("service", "Inconnu")
print(f"1. Service à contacter : {service_contact}")

# 2. Mise à jour : Modifier la valeur d'une clé
rapport_incident["statut"] = "En cours"
print(f"2. Nouveau statut : {rapport_incident['statut']}")

# 3. Itération professionnelle : Parcourir les clés et les valeurs
print("3. Récapitulatif des Champs Principaux:")
for cle, valeur in rapport_incident.items():
    if isinstance(valeur, str): # Filtrer les valeurs qui sont des chaînes de caractères
        print(f"   - {cle.upper():<20} : {valeur}")
```

### 🧪 TP EXPRESS : Fusion de Données (15 min)

**Consigne :** Vous avez deux dictionnaires, `infos_base` et `parametres_supplementaires`. Fusionnez-les dans un seul dictionnaire `profil_complet`.

```python
infos_base = {"nom": "Kamga", "age": 25}
parametres_supplementaires = {"ville": "Douala", "experience": "Junior"}

# Utiliser l'opérateur de fusion {**dict1, **dict2} ou le plus récent dict1 | dict2
# Votre code ici...
# profil_complet = ...
# Résultat attendu : {'nom': 'Kamga', 'age': 25, 'ville': 'Douala', 'experience': 'Junior'}
```

-----

## 3\. ⚡ Efficacité : Les Compréhensions (60 min)

Les compréhensions sont l'outil clé du développeur Python professionnel. Elles transforment les données en une seule ligne, rendant le code plus rapide et lisible.

### Défi 3 : Filtrage et Transformation de Données

**Objectif :** Remplacer une boucle `for` de 5 lignes par une compréhension en une seule ligne pour filtrer et transformer une liste.

#### 📝 Code Guidé : Compréhension de Liste (List Comprehension)

```python
notes_brutes = [10, 15, 8, 19, 11, 14, 7]

# Tâche : Lister uniquement les notes > 12 et leur ajouter un point de bonus

# Version Classique (À ÉVITER)
# notes_filtrees = []
# for note in notes_brutes:
#     if note > 12:
#         notes_filtrees.append(note + 1)
# print(f"Version classique: {notes_filtrees}")


# Version Professionnelle (List Comprehension)
notes_finales = [
    note + 1 
    for note in notes_brutes 
    if note > 12 # Condition de filtrage (à droite)
]
print(f"1. Version optimisée: {notes_finales}")
# Sortie: [16, 20, 15] 
```

#### 📝 Code Guidé : Compréhension de Dictionnaire (Dict Comprehension)

```python
# Tâche : Créer un dictionnaire de codes où les produits déclassés (prix < 50) sont ignorés.

codes_produits = [("X1", 120), ("Y2", 45), ("Z3", 210), ("D4", 30)]

inventaire_clean = {
    code: prix 
    for code, prix in codes_produits 
    if prix >= 50 # Condition de filtrage
}
print(f"2. Inventaire nettoyé: {inventaire_clean}")
# Sortie: {'X1': 120, 'Z3': 210}
```

### 🧪 TP INTÉGRATEUR : Fusion et Filtrage (15 min)

**Consigne :** Vous avez une liste de dictionnaires représentant des serveurs.

1.  Filtrer uniquement les serveurs qui ont un `statut` égal à `'Actif'`.
2.  Créer une **Compréhension de Dictionnaire** qui mappe l'`id` du serveur à son `ip` (uniquement pour les serveurs actifs).

<!-- end list -->

```python
serveurs = [
    {"id": 101, "ip": "192.168.1.10", "statut": "Actif"},
    {"id": 102, "ip": "192.168.1.11", "statut": "Inactif"},
    {"id": 103, "ip": "192.168.1.12", "statut": "Actif"}
]
# Votre code (en une seule ligne de compréhension) ici...
# Résultat attendu : {101: '192.168.1.10', 103: '192.168.1.12'}
```

-----

## ⏳ Conclusion de Session (15 min)

  * **Revue de Code :** Correction et discussion sur la performance et la lisibilité des compréhensions.
  * **Préparation S4 :** Introduction à la **Gestion des Erreurs (`try/except`)** et au **module `random`**. La dernière semaine du Mois 1 sera dédiée à la **robustesse** et au premier projet complet.