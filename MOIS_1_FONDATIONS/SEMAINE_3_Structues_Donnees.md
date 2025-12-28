# 🛠️ MOIS_1_FONDATIONS/SEMAINE_3_Structures_Donnees.md : SEMAINE 3 : Structures de Données

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Sécurité/Efficacité** | Gérer des listes et des tuples. | Maîtrise de la **mutabilité**. |
| **Modélisation** | Représenter un objet complexe avec des dictionnaires. | Utilisation des **dictionnaires** (`dict`). |
| **Optimisation** | Réduire les lignes avec les compréhensions. | Maîtrise des **Compréhensions**. |

-----

## 1. 📦 Séquences : Listes et Tuples (45 min)

### Défi 1 : Gestion d'Inventaire

**Objectif :** Utiliser une liste (mutable) et un tuple (immutable).

#### 📝 Code Guidé : Mutabilité

```python
# --- Listes (Mutables) ---
inventaire = ["Rotor X1", "Capteur Z", "Vanne A"]
inventaire.append("Filtre H9")  # Ajout
inventaire.remove("Capteur Z")  # Suppression
print(f"Inventaire : {inventaire}")

# --- Tuples (Immutables) ---
coordonnees = (48.8584, 2.2945)
# coordonnees[0] = 49.0  # ERREUR attendue
lat, lon = coordonnees  # Déstructuration (Unpacking)
print(f"Lat: {lat}, Lon: {lon}")
```

> [!IMPORTANT]
> **Deep Dive : Listes vs Tuples en mémoire**  
> Les listes sont des tableaux dynamiques : Python réserve un peu plus de place que nécessaire pour permettre des ajouts rapides. Les tuples sont alloués avec une taille fixe exacte, ce qui les rend légèrement plus légers et plus rapides à parcourir.

---

## 2. 🗺️ Mapping : Dictionnaires (60 min)

### Défi 2 : Rapport d'Incident

**Objectif :** Modéliser avec un dictionnaire incluant des données imbriquées.

#### 📝 Code Guidé : Dictionnaires

```python
rapport = {
    "id": "INC-2025",
    "gravite": "Haute",
    "details": {
        "auteur": "Durand",
        "service": "Maintenance"
    },
    "actions": ["Isoler", "Diagnostiquer"]
}

# Accès sécurisé via .get() pour éviter KeyError
service = rapport.get("details", {}).get("service", "Inconnu")
rapport["statut"] = "En cours"

for cle, valeur in rapport.items():
    print(f"{cle}: {valeur}")
```

> [!TIP]
> **Pro Tip : Les Ensembles (Sets) pour l'Unicité**  
> Si vous avez une liste avec des doublons `[1, 2, 2, 3]` et que vous voulez les éléments uniques, utilisez `set()`.  
> `uniques = list(set(ma_liste))`. C'est l'un des moyens les plus rapides en Python pour dédoublonner.

---

## 3. ⚡ Efficacité : Les Compréhensions (60 min)

### Défi 3 : Transformation

**Objectif :** Remplacer une boucle par une compréhension.

#### 📝 Code Guidé : Compréhension de Liste

```python
notes = [10, 15, 8, 19, 11]
# Filtrer les notes > 12 et ajouter 1
finales = [n + 1 for n in notes if n > 12]
print(f"Optimisé : {finales}")
```

> [!WARNING]
> **Piège Courant : Shallow vs Deep Copy**  
> `liste_a = [1, [2, 3]]`  
> `liste_b = liste_a.copy()`  
> Si vous modifiez `liste_b[1][0] = 99`, alors `liste_a[1][0]` changera aussi !  
> *Solution :* Pour copier des structures complexes (listes dans des listes), utilisez `import copy` puis `copy.deepcopy()`.

---

## 🧪 TP SUPPLÉMENTAIRES (Pour aller plus loin)

### Exercice 1 : Analyse de Fréquence
Écrivez un script qui prend une phrase et compte l'occurrence de chaque mot à l'aide d'un dictionnaire.
*Exemple :* "le chat mange le rat" -> `{"le": 2, "chat": 1, ...}`

### Exercice 2 : Gestion de Stock Premium
1. Créez un dictionnaire où la clé est le nom d'un produit et la valeur est un autre dictionnaire `{prix: float, quantite: int}`.
2. Écrivez une fonction qui calcule la valeur totale du stock.
3. Écrivez une ligne (compréhension) qui liste les produits en rupture de stock (`quantite == 0`).

---

## ⏳ Conclusion de Session (15 min)

  * **Revue :** Pourquoi les dictionnaires sont-ils si rapides ? (Grâce au Hachage/Hash Map qui permet un accès quasi-instantané).
  * **Préparation S4 :** Nous rendrons nos scripts indestructibles avec la gestion des exceptions et la lecture de fichiers.
