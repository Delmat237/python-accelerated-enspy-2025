# 🎓 TP 2 - Mois 2 : POO et Architecture (Examen Complet)

## 🎯 Objectifs du TP (3h)

Ce TP évalue votre capacité à concevoir une architecture logicielle robuste en utilisant les piliers de la POO : Encapsulation, Héritage, Polymorphisme. Vous devrez également valider votre code par des tests unitaires automatisés.

---

## 1. Encapsulation : Gestion d'Hôpital (45 min)
**Scénario :** Concevez une classe `Patient` pour un hôpital à Yaoundé.

- Attributs privés : `__id`, `__nom`, `__dossier_medical` (liste).
- Utilisez `@property` pour accéder au nom.
- Implémentez un setter pour le nom qui vérifie qu'il n'est pas vide.
- Méthode `ajouter_diagnostic(info)` pour remplir le dossier.

```python
class Patient:
    def __init__(self, id_patient, nom):
        # Votre code ici...
```

---

## 2. Héritage et Polymorphisme : Flotte de Transport (1h)
**Scénario :** Une agence de voyage camerounaise gère différents types de véhicules.

- Classe Mère : `Vehicule` avec méthode `calculer_tarif(distance)`.
- Sous-classes : `Bus` et `VoitureVIP`.
- `Bus` : Tarif fixe de 500 FCFA/km.
- `VoitureVIP` : Tarif de 1200 FCFA/km + service de bord (2000 FCFA).
- Utilisez `super()` dans les constructeurs.

---

## 3. Méthodes de Classe et Statiques : Gestion Financière (30 min)
**Scénario :** Créez une classe `CompteBancaire`.

- Attribut de classe : `taux_interet = 0.03`.
- Méthode de classe : `modifier_taux(nouveau_taux)`.
- Méthode statique : `est_numero_valide(numero)` (vérifie si 10 chiffres).

---

## 4. Tests Unitaires : Validation des Calculs (45 min)
**Scénario :** Testez votre système de transport avec `pytest`.

- Créez une fixture pour un `Bus`.
- Testez le calcul du tarif pour une distance normale.
- Testez que le tarif ne peut pas être négatif (levez une `ValueError`).

---

## 🏆 Projet Final : Système de Gestion de Bibliothèque (1h)
**Consigne :**
Créez un système avec :
1. Une classe `Livre` (Encapsulation).
2. Une classe `LivreNumerique` qui hérite de `Livre`.
3. Une classe `Bibliotheque` qui gère une liste de livres.
4. Un fichier de test `test_bibliotheque.py` validant l'ajout et l'emprunt.

---

## 🚀 Procédure de Soumission (Git)

1. **Cloner le dépôt :**
   `git clone https://github.com/club-genie-informatique-enspy/TP-PYTHON-TRAINING.git`
2. **Créer une branche :**
   `git checkout -b tp_python/tp2-<votre-nom>-<votre-prenom>`
3. **Commiter :**
   `git commit -m "tp_python(tp2): ajout gestionnaire hospitalier et transport"`
4. **Push & PR :**
   Envoyez vers GitHub et créez une **Pull Request** vers `main`.
