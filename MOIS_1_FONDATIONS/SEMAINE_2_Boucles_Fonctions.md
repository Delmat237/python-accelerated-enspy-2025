# 🛠️ MOIS_1_FONDATIONS/SEMAINE_2_Boucles_Fonctions.md : SEMAINE 2 : Boucles et Fonctions

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Automatisation** | Traiter des listes ou simuler un processus itératif. | Maîtrise de **`for`**, **`while`**, **`range()`**, **`break`/`continue`**. |
| **Modularité** | Créer des blocs de code réutilisables et documentés. | Utilisation de **`def`**, **`return`**, **arguments nommés** (PEP 257). |
| **Avancé** | Fonction acceptant un nombre variable d'arguments. | Introduction à **`*args`** et au **Scope**. |

-----

## 1. 🔄 L'Automatisation : Les Boucles (60 min)

Les boucles permettent d'exécuter une tâche répétitive efficacement.

### Défi 1 : Suivi de Production

**Objectif :** Simuler l'inspection de 10 lots avec `break` et `continue`.

#### 📝 Code Guidé : `for`, `break` et `continue`

```python
# États : (1: OK, 0: Défectueux, -1: Raté)
etats_inspection = [1, 1, 0, 1, -1, 1, 1, 0, 1, 1]

print("--- Début du Contrôle Qualité ---")

for numero_lot, statut in enumerate(etats_inspection, start=1):
    if statut == 0:
        print(f"❌ Lot n°{numero_lot}: DÉFECTUEUX. Arrêt (break).")
        break
    if statut == -1:
        print(f"⚠️ Lot n°{numero_lot}: Inspection Ratée. Saut (continue).")
        continue
    print(f"✅ Lot n°{numero_lot}: Conforme.")

print("--- Fin du Contrôle Qualité ---")
```

#### 💡 Théorie Détaillée : Itération

| Concept | `for` (Itérateur) | `while` (Conditionnel) |
| :--- | :--- | :--- |
| **Usage** | Parcourir un **itérable** (`list`, `range`). | Tant qu'une condition est vraie. |
| **Risque** | Faible. | Élevé (boucles infinies). |
| **`range()`** | Séquence générée "à la volée" (efficace). | n/a |

> [!WARNING]
> **Piège Courant : Modifier une liste pendant l'itération**  
> Évitez de supprimer des éléments d'une liste sur laquelle vous bouclez directement avec `for`. Cela décale les indices et sautera des éléments.  
> *Solution :* Bouclez sur une copie `for item in ma_liste[:]:` ou utilisez une compréhension de liste.

---

## 2. 🧱 Modularité : Les Fonctions (75 min)

Les fonctions encapsulent une logique précise, la rendant facile à maintenir.

### Défi 2 : Le Calculateur de Rentabilité

**Objectif :** Créer une fonction documentée calculant le bénéfice net.

#### 📝 Code Guidé : `def`, `return` et `docstrings`

```python
def calculer_benefice_net(revenu: float, cout: float, taxe: float = 0.25) -> float:
    """
    Calcule le bénéfice net après taxes.

    Args:
        revenu (float): Revenu brut total.
        cout (float): Dépenses totales.
        taxe (float, optional): Taux d'imposition (default 0.25).

    Returns:
        float: Le bénéfice net calculé.
    """
    if revenu < 0 or cout < 0:
        raise ValueError("Les montants ne peuvent pas être négatifs.")
        
    benefice_brut = revenu - cout
    return benefice_brut * (1 - taxe)

# Appels avec arguments nommés pour plus de clarté
res = calculer_benefice_net(revenu=100000, cout=30000, taxe=0.30)
print(f"Bénéfice Net : {res:.2f}€")
```

> [!TIP]
> **Pro Tip : Type Hinting**  
> Utilisez `:` et `->` (comme ci-dessus) pour indiquer les types attendus. Cela ne bloque pas l'exécution, mais aide énormément les IDE (comme VSCode) à vous suggérer les bonnes méthodes et à détecter les erreurs avant de lancer le code.

---

## 3. 🧠 Avancé : `*args` et Scope (30 min)

### Défi 3 : Calculatrice Flexible

**Objectif :** Utiliser **`*args`** pour un nombre variable de notes.

#### 📝 Code Guidé : `*args`

```python
def calculer_moyenne(matiere: str, *notes: float):
    if not notes:
        return 0
    return sum(notes) / len(notes)

print(f"Moyenne Math : {calculer_moyenne('Math', 12, 14, 16):.2f}")
```

> [!IMPORTANT]
> **Deep Dive : La règle LEGB (Scope)**  
> Python cherche les variables dans cet ordre :  
> 1. **L**ocal : Dans la fonction actuelle.  
> 2. **E**nclosing : Dans la fonction parente (si imbrication).  
> 3. **G**lobal : Au niveau du fichier.  
> 4. **B**uilt-in : Fonctions de base de Python (ex: `len`, `sum`).

---

## 🧪 TP SUPPLÉMENTAIRES (Pour aller plus loin)

### Exercice 1 : Deviner le Nombre
Créez un jeu où l'ordinateur choisit un nombre entre 1 et 100.
Utilisez une boucle `while` pour demander à l'utilisateur de deviner.
Indiquez "Plus grand" ou "Plus petit" jusqu'à ce qu'il trouve.

### Exercice 2 : La Suite de Fibonacci
Écrivez une fonction qui génère les `n` premiers nombres de la suite de Fibonacci.
*Rappel :* Chaque nombre est la somme des deux précédents (0, 1, 1, 2, 3, 5, 8...).

---

## ⏳ Conclusion de Session (15 min)

  * **Revue :** Pourquoi préférer les fonctions aux longs scripts ? (Réutilisabilité, testabilité, lisibilité).
  * **Préparation S3 :** Nous verrons comment organiser des masses de données complexes avec les Dictionnaires.