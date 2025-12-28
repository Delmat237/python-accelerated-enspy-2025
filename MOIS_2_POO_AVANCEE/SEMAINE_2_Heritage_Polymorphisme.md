# MOIS_2_POO_AVANCEE/SEMAINE_2_Heritage_Polymorphisme.md : SEMAINE 2 : Héritage et Polymorphisme

## Objectifs Pédagogiques (3h)

| Objectif | Pourquoi c’est crucial ? |
|---------|--------------------------|
| **Maîtriser l'Héritage** | Éviter la duplication de code en créant des sous-classes spécialisées. |
| **Utiliser `super()`** | Étendre les fonctionnalités de la classe mère sans les écraser totalement. |
| **Comprendre le Polymorphisme** | Utiliser une interface unique pour des objets de types différents. |
| **Composition vs Héritage** | Savoir quand hériter et quand utiliser un objet à l'intérieur d'un autre. |

---

## 1. L’Héritage : Créer des Hiérarchies (1h)

L'héritage permet à une classe (enfant) de récupérer les attributs et méthodes d'une autre (parent).

### Défi 1 : Le Compte Épargne Sécurisé

**Objectif :** Créer un `CompteEpargne` avec une limite de retrait stricte.

#### 📝 Code Guidé : `super()`

```python
from compte_bancaire import CompteBancaire

class CompteEpargne(CompteBancaire):
    def __init__(self, titulaire, solde, taux=0.05):
        super().__init__(titulaire, solde)  # Appelle le __init__ de CompteBancaire
        self.taux = taux

    def retirer(self, montant):
        if montant > 100000:
            print("❌ Limite de retrait dépassée pour un compte épargne.")
            return False
        return super().retirer(montant)
```

> [!IMPORTANT]
> **Deep Dive : Le MRO (Method Resolution Order)**  
> Dans quel ordre Python cherche-t-il une méthode ? Il utilise l'algorithme C3 Linearization. Vous pouvez voir cet ordre en tapant `print(CompteEpargne.mro())`. C'est vital pour l'héritage multiple.

---

## 2. Le Polymorphisme : La Flexibilité (1h)

Le polymorphisme est la capacité d'exécuter la même action sur des objets différents, chacun réagissant à sa manière.

### Défi 2 : Le Gestionnaire de Comptes

```python
comptes = [CompteBancaire("Jean", 1000), CompteEpargne("Marie", 5000)]

for c in comptes:
    c.deposer(100) # Appel identique, mais comportement potentiellement différent
```

> [!TIP]
> **Pro Tip : Les Classes Abstraites (ABC)**  
> Si vous voulez créer une classe parent qui *ne peut pas* être instanciée (un "modèle" pur), utilisez le module `abc`.  
> `from abc import ABC, abstractmethod`. Cela force les enfants à implémenter certaines méthodes obligatoirement.

---

## 3. Composition vs Héritage (30 min)

*   **Héritage ("Est un") :** Une `Moto` *est un* `Vehicule`.
*   **Composition ("A un") :** Une `Voiture` *a un* `Moteur`.

> [!WARNING]
> **Piège Courant : L'Héritage Profond**  
> Évitez de créer des hiérarchies trop profondes (ex: A -> B -> C -> D). Cela rend le code rigide et fragile (le "Fragile Base Class problem"). Préférez la composition si la relation n'est pas une évidence biologique ou logique.

---

## 🧪 TP SUPPLÉMENTAIRES (Pour aller plus loin)

### Exercice 1 : Zoo POO
Créez une classe `Animal` avec une méthode `parler()`.
Créez des sous-classes `Chien` et `Chat` qui redéfinissent `parler()`.
Créez une fonction `faire_parler_animal(animal)` qui accepte n'importe quel `Animal` (C'est du polymorphisme !).

### Exercice 2 : Système de Notification
Créez une classe de base `Notification`.
Créez `EmailNotification` et `SMSNotification`.
Implémentez une méthode `envoyer()` différente pour chaque.
Simulez l'envoi d'une liste de notifications mixtes.

---

## ⏳ Conclusion de Session

  * **Revue :** Quand utiliser `super()` ? (Pour ajouter du comportement sans supprimer l'existant).
  * **Prochaine Semaine :** Nous apprendrons à créer des méthodes liées à la classe elle-même (Méthodes Statiques et de Classe).
