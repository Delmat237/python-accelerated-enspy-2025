# MOIS_2_POO_AVANCEE/SEMAINE_1_Classes_Encapsulation.md : SEMAINE 1 : Classes et Encapsulation

### **Cours Complet – Explications Théoriques Avant le Code**

---

## Objectifs Pédagogiques (3h – Approche Explicative)

| Objectif | Pourquoi c’est crucial ? |
|---------|--------------------------|
| **Comprendre la POO** | Modéliser le monde réel (banque, hôpital, agriculture). |
| **Maîtriser `class` et `__init__`** | Créer des objets réutilisables et cohérents. |
| **Appliquer l’encapsulation** | Protéger les données critiques (ex: solde bancaire). |
| **Utiliser `@property`** | Contrôler l’accès sans casser l’interface publique. |
| **TP Réel** | Construire un **système bancaire complet**. |

---

## 1. Introduction à la POO : Pourquoi ? (30 min – Théorie)

> **"Tout est objet en Python."**  
> Si vous faites `type(5)` ou `type("hello")`, Python vous répondra `<class 'int'>` ou `<class 'str'>`. La POO n'est pas une option, c'est le cœur de Python.

### Problème Réel : Gestion d’un Compte Bancaire

Un compte a des données (solde, titulaire) et des comportements (déposer, retirer).  
Sans POO, les données sont éparpillées. Avec POO, elles sont soudées dans une entité unique : **L'Objet**.

---

## 2. Les Fondamentaux de la Classe (45 min – Théorie + Exemple)

### Qu’est-ce qu’une **Classe** ?

C'est le **moule**. L'**Objet** (ou instance) est le gâteau sorti du moule.

| Concept | Analogie | Code |
|--------|---------|--------|
| **Classe** | Plan d’une voiture | `class Voiture:` |
| **Objet** | Une Toyota spécifique | `ma_voiture = Voiture()` |
| **Attribut** | État (Couleur, Vitesse) | `self.couleur = "Rouge"` |
| **Méthode** | Action (Rouler, Freiner) | `def rouler(self):` |

---

### `self` : Le lien vers l'instance

`self` représente l'objet spécifique qui appelle la méthode. Sans lui, Python ne saurait pas quel solde modifier si vous avez 1000 comptes ouverts.

> [!IMPORTANT]
> **Deep Dive : Le constructeur `__init__`**  
> Ce n'est pas strictement "le créateur" de l'objet (c'est `__new__` qui le fait), mais c'est l'**initialiseur**. Il prépare l'objet juste après sa naissance en lui donnant ses valeurs de départ.

---

## 3. Encapsulation : Protéger les Données (45 min – Théorie)

### Le Concept du "Secret professionnel"

En POO, on ne veut pas que l'utilisateur modifie directement les entrailles de l'objet. On utilise des conventions :

| Préfixe | Signification | Comportement Python |
|--------|-----------|--------|
| `nom` | **Public** | Accessible partout. |
| `_nom` | **Protégé** | *Convention* : "S'il vous plaît, ne touchez pas à ça depuis l'extérieur". |
| `__nom` | **Privé** | **Name Mangling** : Python change le nom interne (ex: `_Compte__nom`) pour rendre l'accès accidentel très difficile. |

---

### `@property` : La Puissance des Getters/Setters

Plutôt que de faire `get_solde()` et `set_solde()`, Python propose une syntaxe élégante :

```python
class Compte:
    def __init__(self):
        self._solde = 0

    @property
    def solde(self):
        return f"{self._solde} FCFA"

    @solde.setter
    def solde(self, valeur):
        if valeur < 0:
            raise ValueError("Solde négatif interdit !")
        self._solde = valeur
```

> [!TIP]
> **Pro Tip : L'interface uniforme**  
> Grâce à `@property`, vous pouvez transformer un simple attribut en une méthode calculée plus tard, sans que les gens qui utilisent votre code n'aient à changer leur façon d'écrire `objet.solde`. C'est la clé de la maintenance à long terme.

---

## 4. TP Intégrateur : Système Bancaire (45 min)

### `compte_bancaire.py` (Extrait enrichi)

```python
class CompteBancaire:
    def __init__(self, titulaire: str, solde_initial: float = 0.0):
        self.titulaire = titulaire
        self._solde = solde_initial
        self.__secret_banque = "Code-123" # Privé (Name mangling)

    def deposer(self, montant: float):
        if montant <= 0:
            raise ValueError("Montant positif requis")
        self._solde += montant
        print(f"Nouveau solde : {self.solde}")

    @property
    def solde(self):
        return self._solde
```

> [!WARNING]
> **Piège Courant : Les Imports Circulaires**  
> Si la classe `Banque` a besoin de `Compte` et que `Compte` a besoin de `Banque`, votre programme va planter.  
> *Solution :* Importez uniquement ce qui est nécessaire à l'intérieur des méthodes, ou utilisez le type-hinting sous forme de chaîne de caractères `"Banque"`.

---

## 🧪 TP SUPPLÉMENTAIRES (Pour aller plus loin)

### Exercice 1 : Gestionnaire de Stock POO
Créez une classe `Produit` avec `nom`, `prix`, et `quantite`.
Utilisez une `@property` pour `prix` qui empêche de fixer un prix inférieur à 100 FCFA.
Ajoutez une méthode `vendre(n)` qui diminue la quantité et affiche une erreur si le stock est insuffisant.

### Exercice 2 : Cercle et Rayon
Créez une classe `Cercle`.
L'attribut est `rayon`.
Ajoutez des propriétés pour `diametre` et `surface` (calculées à la volée).
Si on change le `diametre` via un setter, le `rayon` doit se mettre à jour automatiquement !

---

## ⏳ Conclusion & Préparation Semaine 2

  * **Revue :** Quelle est la différence entre `_var` et `__var` ?
  * **Prochaine Semaine :** Nous verrons comment créer des familles de classes (Héritage) et comment une même commande peut avoir plusieurs effets (Polymorphisme).
