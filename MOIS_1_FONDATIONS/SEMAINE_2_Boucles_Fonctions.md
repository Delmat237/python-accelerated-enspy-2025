# 🛠️ MOIS\_1\_FONDATIONS/SEMAINE\_2\_Boucles\_Fonctions.md : Boucles et Fonctions - L'Automatisation

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Automatisation** | Écrire des scripts pour traiter chaque élément d'une liste ou simuler un processus itératif. | Maîtrise de **`for`**, **`while`**, **`range()`**, **`break`/`continue`**. |
| **Modularité** | Créer des blocs de code réutilisables, documentés et avec des signatures claires. | Utilisation de **`def`**, **`return`**, **arguments nommés** (PEP 257). |
| **Avancé** | Concevoir une fonction acceptant un nombre variable d'arguments. | Introduction à **`*args`** et au concept de **Scope**. |

-----

## 1\. 🔄 L'Automatisation : Les Boucles (60 min)

Les boucles permettent d'exécuter une tâche répétitive efficacement sans dupliquer le code.

### Défi 1 : Suivi de Production Séquencé

**Objectif :** Simuler l'inspection de 10 lots de production, signaler un lot défectueux avec `break` et ignorer un lot avec `continue`.

#### 📝 Code Guidé : `for`, `break` et `continue`

```python
# Liste simulant l'état des lots (1: OK, 0: Défectueux, -1: Inspection ratée)
etats_inspection = [1, 1, 0, 1, -1, 1, 1, 0, 1, 1]

print("--- Début du Contrôle Qualité ---")

# Utiliser enumerate() est idiomatique pour obtenir à la fois l'index et la valeur
for numero_lot, statut in enumerate(etats_inspection, start=1):
    if statut == 0:
        print(f"❌ Lot n°{numero_lot}: DÉFECTUEUX. Arrêt immédiat (break).")
        # break sort immédiatement de la boucle
        break
    if statut == -1:
        print(f"⚠️ Lot n°{numero_lot}: Inspection Ratée. Passage au suivant (continue).")
        # continue passe immédiatement à l'itération suivante
        continue
    print(f"✅ Lot n°{numero_lot}: Conforme. Poursuite...")

print("--- Fin du Contrôle Qualité ---")
```

#### 💡 Théorie Détaillée : Les Paradigmes d'Itération

| Concept | `for` (Itérateur) | `while` (Conditionnel) |
| :--- | :--- | :--- |
| **Usage Principal** | Idéal pour itérer sur un **itérable** (`list`, `range`, `dict`). Utiliser **`enumerate()`** est la bonne pratique pour suivre l'index. | Idéal lorsque le **nombre d'itérations est inconnu** et dépend d'une condition externe (`tant que le solde est > 0`). |
| **Risque** | Faible. L'itération est finie par la taille de la séquence. | Élevé. Nécessite une variable d'incrémentation ou de contrôle pour éviter la **boucle infinie**. |
| **`range()`** | Une séquence générée "à la volée" (paresseuse), très efficace en mémoire. C'est l'équivalent du `for (i=0; i<N; i++)` des autres langages. | Non applicable directement. |
| **Gestion du Flux** | **`break`** (Arrêt total de la boucle) et **`continue`** (Saut de l'itération actuelle). | Idem. |

-----

## 2\. 🧱 Modularité : Les Fonctions (75 min)

Les fonctions sont la base de la **modularité** et de la **réutilisabilité** du code. Elles encapsulent une logique précise, la rendant facile à tester et à maintenir.

### Défi 2 : Le Calculateur de Rentabilité (Réutilisable)

**Objectif :** Créer une fonction calculant le bénéfice net après taxes, avec documentation (PEP 257) et arguments nommés.

#### 📝 Code Guidé : `def`, `return` et `docstrings`

```python
def calculer_benefice_net(revenu: float, cout_exploitation: float, taux_taxe: float = 0.25) -> float:
    """
    Calcule le bénéfice net après application d'un taux de taxe.
    (Conforme PEP 257 pour la documentation)

    Args:
        revenu (float): Le revenu brut généré.
        cout_exploitation (float): Les dépenses totales de l'entreprise.
        taux_taxe (float, optional): Le taux de taxe à appliquer. Par défaut à 25%.

    Returns:
        float: Le bénéfice net après taxes.
    """
    # Validation minimale (Robustesse M1/S1)
    if revenu < 0 or cout_exploitation < 0:
        raise ValueError("Les montants ne peuvent pas être négatifs.")
        
    benefice_brut = revenu - cout_exploitation
    taxe = benefice_brut * taux_taxe
    
    # return est obligatoire pour que le résultat soit exploitable en dehors de la fonction
    return benefice_brut - taxe

# Appels professionnels
resultat_1 = calculer_benefice_net(100000, 30000, 0.30)
# Utilisation d'arguments nommés pour une clarté maximale
resultat_2 = calculer_benefice_net(cout_exploitation=25000, revenu=50000) 

print(f"Résultat A (30% taxe): {resultat_1:.2f}€")
print(f"Résultat B (25% taxe): {resultat_2:.2f}€")
```

#### 💡 Théorie Détaillée : Les Règles de la Modularité

| Concept | Explication Détaillée | Règle du Coder |
| :--- | :--- | :--- |
| **`return`** | Termine l'exécution de la fonction et renvoie une ou plusieurs valeurs à l'appelant. Sans `return` explicite, la fonction renvoie implicitement **`None`**. | **Ne pas `print` le résultat d'un calcul dans une fonction**; toujours le `return` pour que la valeur soit utilisable par d'autres fonctions. |
| **`Docstrings` (PEP 257)** | La documentation doit être située juste après la signature de la fonction. Elle est accessible via `help(ma_fonction)`. | **Obligatoire.** Doit expliquer le rôle, l'usage des arguments (`Args`) et la valeur de retour (`Returns`). |
| **Arguments Nommés** | Utiliser `cle=valeur` lors de l'appel (ex: `fonction(taux_taxe=0.30)`). Le code devient **auto-documenté**, le rôle de chaque valeur passée est clair. | **Bonne Pratique.** À privilégier, surtout si une fonction a plus de deux arguments. |

-----

## 3\. 🧠 Avancé : `*args` et Scope (30 min)

### Défi 3 : La Calculatrice de Moyenne Flexible

**Objectif :** Créer une fonction calculant la moyenne d'un nombre variable de notes avec **`*args`**.

#### 📝 Code Guidé : L'opérateur `*args`

```python
def calculer_moyenne_generale(nom_matiere: str, *notes: float):
    """Calcule la moyenne d'un nombre illimité de notes pour une matière donnée."""
    # 'notes' est automatiquement agrégé en un tuple
    
    if not notes:
        print(f"Attention : Aucune note fournie pour {nom_matiere}.")
        return 0
        
    somme = sum(notes) 
    nombre_notes = len(notes)
    
    print(f"Moyenne pour {nom_matiere} sur {nombre_notes} notes...")
    return somme / nombre_notes

# Tests flexibles
print(f"Moyenne Math : {calculer_moyenne_generale('Mathématiques', 12, 14, 16):.2f}")
print(f"Moyenne Info : {calculer_moyenne_generale('Informatique', 18, 17, 15, 12, 11):.2f}")
```

### 🧪 TP EXPRESS : Scope Local vs. Global (15 min)

**Consigne :** Analysez et exécutez ce code pour comprendre le Scope.

```python
taux_global = 100  # Variable globale

def ma_fonction():
    # Si on écrit : taux_global = 50, cela crée une NOUVELLE variable LOCALE
    taux_local = 50  
    print(f"Dans la fonction, le taux local est: {taux_local}")

ma_fonction()
print(f"En dehors, le taux global est: {taux_global}")
# Le taux global est resté 100.
```

#### 💡 Théorie Détaillée : Le Scope (Portée)

| Concept | Explication Détaillée | Conséquence |
| :--- | :--- | :--- |
| **Scope Local** | Espace de nom créé lors de l'appel de la fonction. Toutes les variables définies à l'intérieur sont **détruites** à la fin de la fonction (sauf si elles sont retournées). | La modification d'une variable globale *sans* le mot-clé `global` crée une nouvelle variable locale portant le même nom. **Séparation claire des responsabilités.** |
| **Scope Global** | Espace de nom au niveau du module (fichier). Les variables ici sont accessibles par toutes les fonctions du fichier. | Les fonctions peuvent **lire** les variables globales, mais ne peuvent les **modifier** sans utiliser le mot-clé `global` (pratique généralement découragée). |
| **`*args` (Arguments Variable)** | Agrège tous les arguments positionnels restants (ceux sans mot-clé) dans un **tuple**. Utilisé pour les fonctions qui nécessitent un nombre flexible d'entrées. | Le résultat est toujours un **tuple** (immutable), permettant une itération simple. |

-----

## ⏳ Conclusion de Session (15 min)

  * **Revue de Code :** Correction des TP, insistance sur la bonne utilisation de `break` vs. `continue` et la validation du concept de Scope.
  * **Préparation S3 :** Étudier **listes**, **dictionnaires**, **tuples** et **compréhensions**. La semaine prochaine sera dédiée à la **manipulation efficace des données**, essentielle pour la Data Science et les APIs.