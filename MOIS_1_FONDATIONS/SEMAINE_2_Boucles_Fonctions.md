
# 🛠️ MOIS 1 / SEMAINE 2 : Boucles et Fonctions - L'Automatisation

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Automatisation** | Écrire des scripts pour traiter chaque élément d'une liste ou simuler un processus itératif. | Maîtrise de `for`, `while`, `range()`, `break`/`continue`. |
| **Modularité** | Créer des blocs de code réutilisables, documentés et avec des signatures claires. | Utilisation de `def`, `return`, arguments nommés. |
| **Avancé** | Concevoir une fonction acceptant un nombre variable d'arguments. | Introduction à `*args` et au concept de **Scope**. |

-----

## 1\. 🔄 L'Automatisation : Les Boucles (60 min)

Les boucles sont l'essence de la programmation : elles permettent d'exécuter la même tâche plusieurs fois sans répéter le code.

### Défi 1 : Suivi de Production Séquencé

**Objectif :** Simuler l'inspection d'une série de 10 lots de production, en signalant immédiatement un lot défectueux et en ignorant un lot dont l'inspection a échoué (sans arrêter la chaîne).

#### 📝 Code Guidé : `for`, `break` et `continue`

Nous allons utiliser `range()` pour le nombre de lots, et `break` et `continue` pour gérer les exceptions du processus.

```python
# Liste simulant l'état de l'inspection (1: OK, 0: Défectueux, -1: Inspection ratée)
etats_inspection = [1, 1, 0, 1, -1, 1, 1, 0, 1, 1]

print("--- Début du Contrôle Qualité ---")

for numero_lot, statut in enumerate(etats_inspection):
    # L'utilisation d'enumerate() est une bonne pratique pour obtenir l'index
    
    if statut == 0:
        print(f"❌ Lot n°{numero_lot + 1}: DÉFECTUEUX. Arrêt immédiat de la chaîne (break).")
        # Arrête toute la boucle et passe à la suite du programme
        break 

    if statut == -1:
        print(f"⚠️ Lot n°{numero_lot + 1}: Inspection Ratée. On passe au suivant (continue).")
        # Saute le reste du code dans cette itération et passe au lot suivant
        continue 

    # Ce code n'est exécuté que si statut est 1
    print(f"✅ Lot n°{numero_lot + 1}: Conforme. Poursuite...")

print("--- Fin du Contrôle Qualité ---")

# Défi d'extension : Remplacer la boucle for par une boucle while qui compte de 10 à 0.
```

#### 💡 Théorie Brève : Le "Comment" du `for` et du `while`

  * **`for` (Itération) :** Idéal quand vous savez **combien de fois** (sur une séquence) vous devez boucler. Il est piloté par les données.
  * **`while` (Condition) :** Idéal quand vous ne savez **pas combien de fois** vous devez boucler, mais vous connaissez la condition de sortie (ex: "tant que le solde n'est pas nul").

-----

## 2\. 🧱 Modularité : Les Fonctions (75 min)

Les fonctions sont la première étape vers la **modularité** et la **réutilisation du code**.

### Défi 2 : Le Calculateur de Rentabilité (Réutilisable)

**Objectif :** Créer une fonction qui calcule un bénéfice après taxes, en s'assurant que la fonction soit bien documentée (`docstring`) et que les arguments soient clairs (nommés).

#### 📝 Code Guidé : `def`, `return` et `docstrings`

```python
# Bonnes pratiques : utiliser un docstring pour expliquer ce que fait la fonction
def calculer_benefice_net(revenu, cout_exploitation, taux_taxe=0.25):
    """
    Calcule le bénéfice net après application d'un taux de taxe.

    Args:
        revenu (float): Le revenu brut généré.
        cout_exploitation (float): Les dépenses totales de l'entreprise.
        taux_taxe (float, optional): Le taux de taxe à appliquer. Par défaut à 25%.

    Returns:
        float: Le bénéfice net.
    """
    benefice_brut = revenu - cout_exploitation
    taxe = benefice_brut * taux_taxe
    benefice_net = benefice_brut - taxe
    
    # Utilisation de return pour que le résultat soit exploitable
    return benefice_net

# 1. Appel avec tous les arguments positionnels (ordre important)
resultat_A = calculer_benefice_net(100000, 30000, 0.30)
print(f"Résultat A (Taxe 30%): {resultat_A:.2f}")

# 2. Appel avec arguments nommés (ordre non pertinent, clarté maximale)
resultat_B = calculer_benefice_net(cout_exploitation=25000, revenu=50000) # Utilise la taxe par défaut (0.25)
print(f"Résultat B (Taxe 25%): {resultat_B:.2f}")
```

#### 💡 Théorie Brève : Signature et Arguments

  * **Signature :** La ligne `def nom_fonction(arg1, arg2):` est la carte d'identité de votre fonction.
  * **Arguments Nommés :** Ils rendent le code **auto-documenté**. On sait ce que représente chaque valeur passée. C'est une pratique professionnelle à privilégier.

-----

## 3\. 🧠 Avancé : `*args` et Scope (30 min)

### Défi 3 : La Calculatrice de Moyenne Flexible

**Objectif :** Écrire une fonction capable de calculer la moyenne d'un nombre **quelconque** de notes, sans avoir à lister chaque note dans la signature de la fonction.

#### 📝 Code Guidé : L'opérateur `*args`

L'opérateur **`*args`** (positionnel) agrège tous les arguments non nommés restants dans un **tuple**.

```python
def calculer_moyenne_generale(*notes):
    """Calcule la moyenne d'un nombre illimité de notes."""
    # 'notes' est ici un tuple (même si on l'appelle 'notes')
    
    if not notes: # Gère le cas où aucun argument n'est passé
        return 0
        
    somme = sum(notes) # Fonction built-in pour additionner les éléments d'un itérable
    nombre_notes = len(notes)
    
    return somme / nombre_notes

# Appels flexibles
print(f"Moyenne Simple: {calculer_moyenne_generale(12, 14, 16):.2f}")
print(f"Moyenne Longue: {calculer_moyenne_generale(18, 17, 15, 12, 11):.2f}")
```

### 🧪 TP EXPRESS : Scope Local vs. Global (15 min)

**Consigne :** Déterminez le résultat de ce script en comprenant le concept de portée (Scope), puis vérifiez en l'exécutant.

```python
x = 100 # Variable Globale

def ma_fonction():
    x = 50 # Variable Locale (Création d'une nouvelle variable x dans le scope local)
    print(f"Dans la fonction, x est: {x}")

ma_fonction()
print(f"En dehors de la fonction, x est: {x}")
# Quelle valeur de x est affichée à la fin ?
```

-----

## ⏳ Conclusion de Session (15 min)

  * **Revue de Code :** Discussion sur le Scope et la différence entre `for` et `while`.
  * **Préparation S3 :** Introduction aux **Listes, Dictionnaires et Compréhensions**. Le code de la semaine prochaine sera orienté **manipulation de données**.