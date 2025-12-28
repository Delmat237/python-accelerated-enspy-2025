# MOIS_2_POO_AVANCEE/SEMAINE_3_Methodes_Classe_Statiques.md : SEMAINE 3 : Méthodes de Classe et Statiques

## Objectifs Pédagogiques (3h)

| Objectif | Pourquoi c’est crucial ? |
|---------|--------------------------|
| **Comprendre `@classmethod`** | Manipuler des données liées à la classe elle-même. |
| **Utiliser `@staticmethod`** | Créer des fonctions utilitaires logiquement regroupées. |
| **Le Factory Pattern** | Savoir créer des objets de différentes manières élégantes. |
| **Gérer les Attributs de Classe** | Partager des informations entre toutes les instances de façon sécurisée. |

---

## 1. Méthodes de Classe : L'Information Partagée (1h)

Une méthode de classe reçoit la classe elle-même (`cls`) en premier argument.

### Défi 1 : Le Compteur de Comptes Global

**Objectif :** Suivre le nombre total de comptes créés dans toute la banque.

#### 📝 Code Guidé : `@classmethod`

```python
class Banque:
    nombre_total_comptes = 0 # Attribut de classe

    def __init__(self, titulaire):
        self.titulaire = titulaire
        Banque._incrementer_compteur()

    @classmethod
    def _incrementer_compteur(cls):
        cls.nombre_total_comptes += 1

    @classmethod
    def afficher_stats(cls):
        print(f"La banque gère {cls.nombre_total_comptes} comptes au total.")
```

> [!TIP]
> **Pro Tip : Le Pattern "Factory"**  
> Les méthodes de classe sont parfaites pour créer des objets avec des données différentes.  
> `Compte.depuis_json(donnees_brutes)` ou `Date.aujourd_hui()`. Cela permet d'avoir plusieurs "constructeurs" nommés.

---

## 2. Méthodes Statiques : Les Utilitaires (1h)

Une méthode statique est une fonction qui n'a besoin ni de `self` ni de `cls`, mais qui appartient logiquement à la classe.

### Défi 2 : Validateur de Devises

#### 📝 Code Guidé : `@staticmethod`

```python
class FinanceUtils:
    @staticmethod
    def est_devise_valide(devise):
        return devise.upper() in ["FCFA", "EUR", "USD"]
```

> [!IMPORTANT]
> **Deep Dive : Comparaison des Méthodes**
>
> | Type | Décorateur | Premier Arg | Accès |
| :--- | :--- | :--- | :--- |
| **Instance** | Aucun | `self` | Attributs de l'objet |
| **Classe** | `@classmethod` | `cls` | Attributs de la classe |
| **Statique** | `@staticmethod` | Aucun | Aucun (indépendante) |

---

## 3. Quand utiliser quoi ? (30 min)

> [!WARNING]
> **Piège Courant : Utiliser `@staticmethod` à l'excès**  
> Si votre méthode statique n'a aucun lien logique avec la classe, il vaut mieux en faire une simple fonction en haut de votre fichier. `@staticmethod` ne doit être utilisé que pour regrouper des utilitaires qui font sens *dans* le contexte de la classe.

---

## 🧪 TP SUPPLÉMENTAIRES (Pour aller plus loin)

### Exercice 1 : Convertisseur de Température
Créez une classe `Temperature`.
Ajoutez une méthode de classe `depuis_fahrenheit(valeur)` qui retourne une instance de `Temperature` convertie en Celsius.
Ajoutez une méthode statique `est_froid(celsius)` qui retourne `True` si la température est < 10.

### Exercice 2 : Gestionnaire d'Utilisateurs
Créez une classe `Utilisateur`. 
Ajoutez un attribut de classe `utilisateurs_actifs` (une liste).
Chaque fois qu'un utilisateur est créé, il est ajouté à la liste via une méthode de classe.
Ajoutez une méthode de classe `trouver_utilisateur(nom)` qui cherche dans la liste globale.

---

## ⏳ Conclusion de Session

  * **Revue :** Pourquoi utiliser `cls` au lieu du nom de la classe en dur ? (Pour que l'héritage fonctionne correctement !).
  * **Prochaine Semaine :** Nous poserons la cerise sur le gâteau : les Tests Unitaires pour garantir la qualité de notre code.
