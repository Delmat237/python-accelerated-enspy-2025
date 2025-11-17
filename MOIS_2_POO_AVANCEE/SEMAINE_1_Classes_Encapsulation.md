# MOIS_2_POO_AVANCEE/SEMAINE_1_Classes_Encapsulation.md  
### **Cours Complet – Explications Théoriques Avant le Code**

---

## Objectifs Pédagogiques (3h – Approche Explicative)

| Objectif | Pourquoi c’est crucial ? |
|---------|--------------------------|
| **Comprendre la POO** | Modéliser le monde réel (banque, hôpital, agriculture) |
| **Maîtriser `class` et `__init__`** | Créer des objets réutilisables |
| **Appliquer l’encapsulation** | Protéger les données critiques (ex: solde bancaire) |
| **Utiliser `@property`** | Contrôler l’accès sans casser l’interface |
| **TP Réel** | Construire un **système bancaire complet** |

---

## 1. Introduction à la POO : Pourquoi ? (30 min – Théorie)

> **Avant le code, on comprend le besoin.**

### Problème Réel : Gestion d’un Compte Bancaire

Imaginez un **système bancaire** au Cameroun (MTN MoMo, Orange Money, ou banque classique).  
Un compte a :
- Un **titulaire** (nom)
- Un **solde** (argent)
- Des **opérations** (dépôt, retrait)
- Un **historique**

---

### Sans POO → Code Spaghettis

```python
# 5 variables globales
titulaire1 = "Kamga"
solde1 = 50000
historique1 = []

titulaire2 = "Njoya"
solde2 = 100000
historique2 = []

# 10 fonctions
def deposer1(montant): ...
def deposer2(montant): ...
# → 20 fonctions, code dupliqué, erreurs faciles
```

**Problèmes** :
- Code **dupliqué**
- Risque d’erreur (solde1 modifié par erreur)
- Impossible à maintenir

---

### Avec POO → Code Propre, Sûr, Évolutif

```python
compte1 = CompteBancaire("Kamga", 50000)
compte2 = CompteBancaire("Njoya", 100000)

compte1.deposer(20000)
compte2.retirer(15000)
```

**Avantages** :
- **Une seule classe** → réutilisable
- **Données protégées** → pas d’accès direct au solde
- **Évolutif** → ajouter `CompteEpargne`, `CompteCourant`

---

## 2. Les Fondamentaux de la Classe (45 min – Théorie + Exemple)

### Qu’est-ce qu’une **Classe** ?

> **Un plan de construction** pour créer des objets.

| Concept | Analogie | Exemple |
|--------|---------|--------|
| **Classe** | Plan d’une voiture | `class CompteBancaire` |
| **Objet** | Voiture construite | `compte = CompteBancaire(...)` |
| **Attribut** | Caractéristique | `titulaire`, `solde` |
| **Méthode** | Action | `deposer()`, `retirer()` |

---

### `self` : Qui suis-je ?

```python
def deposer(self, montant):
    self.solde += montant  # ← "mon" solde
```

- `self` = **l’objet courant**
- Permet de distinguer `compte1.solde` de `compte2.solde`

---

### `__init__` : Le Constructeur

```python
def __init__(self, titulaire, solde_initial=0):
    self.titulaire = titulaire
    self._solde = solde_initial
```

- Appelé **automatiquement** à la création
- Initialise les attributs

---

## 3. Encapsulation : Protéger les Données (45 min – Théorie)

> **Ne pas laisser n’importe qui toucher au solde !**

### Niveaux de Protection

| Préfixe | Visibilité | Exemple |
|--------|-----------|--------|
| `public` | Tout le monde | `self.titulaire` |
| `_protegé` | Convention (interne) | `self._solde` |
| `__prive` | Name mangling | `self.__historique` |

---

### `@property` : Accès Contrôlé

```python
@property
def solde(self):
    return self._solde  # Lecture OK

@solde.setter
def solde(self, valeur):
    raise AttributeError("Interdit !")
```

**Pourquoi ?**
- Empêche : `compte.solde = -1000`
- Force l’usage de `deposer()` / `retirer()`

---

## 4. Représentation des Objets (15 min)

| Méthode | Usage |
|--------|-------|
| `__str__` | Affichage utilisateur (`print(obj)`) |
| `__repr__` | Débogage (`repr(obj)`) |

---

## 5. TP Intégrateur : Système Bancaire (45 min – Explication Avant Code)

### Objectif du TP

Construire un **système bancaire complet** avec :
- Classe `CompteBancaire`
- Encapsulation totale
- Historique des transactions
- Relevé bancaire formaté
- Intérêts annuels

---

### Structure du Projet

```bash
TP_Systeme_Bancaire/
├── compte_bancaire.py     ← Class POO
└── main.py                ← Démonstration
```

---

## 6. Code Complet (Après la Théorie)

> **Maintenant que tout est clair, voici le code.**

### `compte_bancaire.py`

```python
from datetime import datetime
from typing import List, Dict

class CompteBancaire:
    """Représente un compte bancaire sécurisé."""
    
    # Attribut de classe
    taux_interet = 0.03  # 3% annuel

    def __init__(self, titulaire: str, solde_initial: float = 0.0):
        """Crée un nouveau compte."""
        self.titulaire = titulaire
        self._solde = max(solde_initial, 0)  # Pas de solde négatif
        self.__historique: List[Dict] = []
        self._ajouter_transaction("Création", self._solde)

    def _ajouter_transaction(self, type_op: str, montant: float):
        """Enregistre une opération dans l'historique (privé)."""
        self.__historique.append({
            "date": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
            "type": type_op,
            "montant": montant,
            "solde": self._solde
        })

    def deposer(self, montant: float) -> bool:
        """Dépose de l'argent."""
        if not self.est_montant_valide(montant):
            raise ValueError("Montant doit être positif")
        self._solde += montant
        self._ajouter_transaction("Dépôt", montant)
        return True

    def retirer(self, montant: float) -> bool:
        """Retire de l'argent si fonds suffisants."""
        if not self.est_montant_valide(montant):
            raise ValueError("Montant invalide")
        if montant > self._solde:
            raise ValueError(f"Fonds insuffisants: {self._solde:,.2f} FCFA")
        self._solde -= montant
        self._ajouter_transaction("Retrait", -montant)
        return True

    @property
    def solde(self) -> float:
        """Lecture seule du solde."""
        return self._solde

    @property
    def historique(self) -> List[Dict]:
        """Historique en lecture seule."""
        return self.__historique.copy()

    def generer_releve(self) -> str:
        """Génère un relevé bancaire formaté."""
        lignes = [f"Relevé de {self.titulaire}", "="*60]
        for t in self.__historique:
            signe = "+" if t["montant"] >= 0 else ""
            lignes.append(
                f"{t['date']} | {t['type']:8} | {signe}{t['montant']:8.2f} | "
                f"Solde: {t['solde']:8.2f}"
            )
        return "\n".join(lignes)

    @classmethod
    def appliquer_interets(cls, compte) -> float:
        """Applique les intérêts annuels."""
        interet = compte._solde * cls.taux_interet
        compte.deposer(interet)
        return interet

    @staticmethod
    def est_montant_valide(montant) -> bool:
        """Vérifie la validité d’un montant."""
        return isinstance(montant, (int, float)) and montant > 0

    def __str__(self) -> str:
        return f"Compte[{self.titulaire}] Solde: {self._solde:,.2f} FCFA"

    def __repr__(self) -> str:
        return f"CompteBancaire('{self.titulaire}', {self._solde})"
```

---

### `main.py`

```python
from compte_bancaire import CompteBancaire

# Création
compte = CompteBancaire("M. Kamga", 50000)

# Opérations
compte.deposer(25000)
compte.retirer(10000)
compte.deposer(30000)

# Intérêts
interet = CompteBancaire.appliquer_interets(compte)

# Affichage
print(compte)
print(f"\nIntérêts gagnés : {interet:,.2f} FCFA")
print("\n" + compte.generer_releve())
```

---

## 7. Conclusion & Préparation Semaine 3

| Ce que vous savez maintenant |
|------------------------------|
| Créer des **classes robustes** |
| **Protéger** les données critiques |
| Utiliser **`@property`** comme un pro |
| Générer des **relevés formatés** |

---

## Prochaine Semaine
> **SEMAINE 2 : Héritage, Polymorphisme, Dunder Methods**  
> `CompteEpargne`, `CompteCourant`, `super()`, `__add__`, etc.

