# MOIS_2_POO_AVANCEE/INTRODUCTION_POO.md

## Introduction à la Programmation Orientée Objet (POO)  
### *Pourquoi la POO est essentielle pour un développeur Python professionnel*

---

### Pourquoi la POO ?

| Problème Réel | Solution POO |
|---------------|--------------|
| Code dupliqué, difficile à maintenir | **Réutilisation** via les classes |
| Données et comportements mélangés | **Encapsulation** : données + méthodes |
| Évolution complexe d’un système | **Héritage** et **Polymorphisme** |
| Projets d’équipe (Flask, Django, APIs) | **Modularité** et **lisibilité** |

> **Exemple concret** : Une pharmacie gère des médicaments, des clients, des factures.  
> Sans POO → 50 fonctions globales → cauchemar.  
> Avec POO → 3 classes claires → propre, évolutif, testable.

---

### Les 4 Piliers de la POO

| Pilier | Définition | Exemple |
|--------|------------|--------|
| **Encapsulation** | Regrouper données + méthodes dans une classe | `class Medicament: def __init__(self, nom, prix): ...` |
| **Abstraction** | Cacher la complexité, montrer l’essentiel | Méthode `.vendre()` sans exposer le stock interne |
| **Héritage** | Réutiliser du code d’une classe mère | `class Antibiotique(Medicament): ...` |
| **Polymorphisme** | Même interface, comportements différents | `.calculer_prix()` différent selon le type |

---

### Utilité en Contexte Camerounais

| Domaine | Application POO |
|--------|------------------|
| **Santé** | Système de gestion hospitalière (Patient, Médecin, Ordonnance) |
| **Agriculture** | Suivi de récoltes (Parcelle, Culture, Rendement) |
| **Finance** | Banque mobile (Compte, Transaction, Client) |
| **Éducation** | Plateforme e-learning (Étudiant, Cours, Note) |

> **Objectif du Mois 2** : Maîtriser la POO pour **construire des systèmes robustes, testables et évolutifs**.

---

### Analogie Simple : La Voiture

```python
class Voiture:
    def __init__(self, marque, vitesse_max):
        self.marque = marque
        self.vitesse_max = vitesse_max
        self.vitesse = 0  # état interne

    def accelerer(self, increment):
        self.vitesse = min(self.vitesse + increment, self.vitesse_max)

    def freiner(self):
        self.vitesse = 0
```

- **Objet** = une voiture spécifique (`ma_toyota = Voiture("Toyota", 180)`)
- **Classe** = le plan de construction
- **Méthodes** = les actions possibles
- **Attributs** = les caractéristiques

---

### POO vs Programmation Fonctionnelle

| POO | Fonctionnelle |
|-----|---------------|
| **État mutable** (objets) | **État immuable** |
| **Classes + méthodes** | **Fonctions pures** |
| Idéal pour **modélisation du monde réel** | Idéal pour **traitement de données** |

> **Python = multi-paradigme** → on combine les deux !

---

### Roadmap du Mois 2 : POO Avancée

```bash
MOIS_2_POO_AVANCEE/
├── INTRODUCTION_POO.md                 ← CE COURS
├── SEMAINE_1_Classes_Encapsulation.md
├── SEMAINE_2_Heritage_Polymorphisme.md
├── SEMAINE_3_Methodes_Classe_Statiques.md
├── SEMAINE_4_Tests_Unitaires_Pytest.md
├── cours_poo_avance.tex
├── tests/
│   └── test_systeme_bancaire.py
└── TP_Systeme_Bancaire/
    └── compte_bancaire.py
```

---

### À la Fin du Mois 2, Vous Saurez :

- Modéliser un système réel avec des classes
- Protéger vos données avec `@property`
- Réutiliser du code avec l’héritage
- Tester automatiquement avec `pytest`
- Écrire du code **propre, professionnel, industriel**

---

**Prochaine Étape** :  
> **SEMAINE 1 : Classes et Encapsulation**  
> `class`, `__init__`, `@property`, setters/getters

