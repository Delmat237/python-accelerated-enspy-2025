# 🛠️ MOIS_1_FONDATIONS/SEMAINE_3_Structures_Donnees.md : Structures de Données et Efficacité

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Sécurité/Efficacité** | Gérer un inventaire modifiable (`list`) et des identifiants non modifiables (`tuple`). | Maîtrise de la **mutabilité** et des méthodes de séquences. |
| **Modélisation** | Représenter un objet complexe (ex: un produit ou un profil utilisateur) avec des paires clé-valeur. | Utilisation professionnelle des **dictionnaires** (`dict`). |
| **Optimisation** | Réduire 5 à 10 lignes de code en une seule ligne élégante et performante. | Maîtrise des **Compréhensions de Liste et de Dictionnaire**. |

-----

## 1\. 📦 Séquences : Listes et Tuples (45 min)

### Défi 1 : Gestion d'Inventaire et de Coordonnées

**Objectif :** Utiliser une liste pour un inventaire modifiable et un tuple pour des coordonnées immuables.

#### 📝 Code Guidé : Mutabilité vs. Immutabilité

```python
# --- Partie 1 : Inventaire Modifiable (Listes) ---
inventaire_produits = ["Rotor X1", "Capteur Z", "Vanne A"]

# Ajouter un produit
inventaire_produits.append("Filtre H9")
print(f"1. Après ajout: {inventaire_produits}")

# Supprimer un produit
inventaire_produits.remove("Capteur Z")
print(f"2. Après suppression: {inventaire_produits}")

# Slicing pour les deux derniers produits
derniers_produits = inventaire_produits[-2:]
print(f"3. Les deux derniers: {derniers_produits}")

print("-" * 20)

# --- Partie 2 : Coordonnées (Tuples Immutables) ---
coordonnees_usine = (48.8584, 2.2945)

# Tentative de modification (doit échouer)
try:
    coordonnees_usine[0] = 49.0
except TypeError as e:
    print(f"4. ERREUR attendue: {e}")

# Déstructuration
lat, lon = coordonnees_usine
print(f"5. Latitude: {lat}, Longitude: {lon}")

# Défi d'extension : Ajouter une vérification de la validité des coordonnées (ex: entre -90 et 90 pour lat)
```

#### 💡 Théorie Brève : Mutabilité vs. Immutabilité

  * **Listes:** Mutables, idéales pour des données dynamiques (ajout, suppression).
  * **Tuples:** Immutables, optimisés pour des données fixes (efficacité et sécurité).

-----

## 2\. 🗺️ Mapping : Dictionnaires (60 min)

### Défi 2 : Modélisation d'un Rapport d'Incident

**Objectif :** Modéliser un rapport d'incident avec un dictionnaire, incluant des données imbriquées, et itérer dessus.

#### 📝 Code Guidé : Accès Sécurisé et Itération

```python
# Rapport d'incident
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

# Accès sécurisé avec .get()
service_contact = rapport_incident.get("details_auteur", {}).get("service", "Inconnu")
print(f"1. Service: {service_contact}")

# Mise à jour du statut
rapport_incident["statut"] = "En cours"
print(f"2. Nouveau statut: {rapport_incident['statut']}")

# Itération sur les clés et valeurs
print("3. Récapitulatif:")
for cle, valeur in rapport_incident.items():
    if isinstance(valeur, str):
        print(f"   - {cle.upper():<20}: {valeur}")

# Défi d'extension : Ajouter une nouvelle action à `actions_necessaires` via append
```

### 🧪 TP EXPRESS : Fusion de Données (15 min)

**Consigne :** Fusionnez `infos_base` et `parametres_supplementaires` dans `profil_complet`.

```python
infos_base = {"nom": "Kamga", "age": 25}
parametres_supplementaires = {"ville": "Douala", "experience": "Junior"}

# Fusion avec l'opérateur |
profil_complet = infos_base | parametres_supplementaires
print(f"Résultat: {profil_complet}")
```

-----

## 3\. ⚡ Efficacité : Les Compréhensions (60 min)

Les compréhensions optimisent le code en le rendant concis et performant.

### Défi 3 : Filtrage et Transformation de Données

**Objectif :** Remplacer une boucle par des compréhensions.

#### 📝 Code Guidé : Compréhension de Liste

```python
notes_brutes = [10, 15, 8, 19, 11, 14, 7]

# Version classique (à éviter)
# notes_filtrees = []
# for note in notes_brutes:
#     if note > 12:
#         notes_filtrees.append(note + 1)
# print(f"Classique: {notes_filtrees}")

# Compréhension
notes_finales = [note + 1 for note in notes_brutes if note > 12]
print(f"1. Optimisé: {notes_finales}")  # [16, 20, 15]

# Défi d'extension : Ajouter une condition pour ignorer les notes < 5
```

#### 📝 Code Guidé : Compréhension de Dictionnaire

```python
codes_produits = [("X1", 120), ("Y2", 45), ("Z3", 210), ("D4", 30)]

# Compréhension
inventaire_clean = {code: prix for code, prix in codes_produits if prix >= 50}
print(f"2. Inventaire: {inventaire_clean}")  # {'X1': 120, 'Z3': 210}
```

### 🧪 TP INTÉGRATEUR : Fusion et Filtrage (15 min)

**Consigne :** Filtrer les serveurs actifs et créer un dictionnaire d'IPs.

```python
serveurs = [
    {"id": 101, "ip": "192.168.1.10", "statut": "Actif"},
    {"id": 102, "ip": "192.168.1.11", "statut": "Inactif"},
    {"id": 103, "ip": "192.168.1.12", "statut": "Actif"}
]

# Compréhension
ips_actifs = {serveur["id"]: serveur["ip"] for serveur in serveurs if serveur["statut"] == "Actif"}
print(f"Résultat: {ips_actifs}")  # {101: '192.168.1.10', 103: '192.168.1.12'}
```

-----

## ⏳ Conclusion de Session (15 min)

  * **Revue de Code:** Analyse des TP, focus sur les performances des compréhensions.
  * **Préparation S4:** Découverte de **gestion des erreurs (`try/except`)** et du **module `random`**. La semaine prochaine portera sur la robustesse et le projet final.

Cette session privilégie la pratique pour maîtriser les structures de données et leur optimisation.

