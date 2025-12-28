# 🎓 TP 1 - Mois 1 : Fondations (Examen Complet)

## 🎯 Objectifs du TP (2h - 3h)

Cette fiche propose des exercices concrets, inspirés de problèmes réels du quotidien ou du domaine de l'ingénierie au Cameroun (ex. : gestion agricole, santé, finance locale, éducation). L'approche est **pratique et code-first** : chaque exercice simule un scénario professionnel pour appliquer les concepts.

**Matériel Requis :** Python 3.11+, IDE (VS Code).

---

## 1. Types de Données : Calculs Agricoles Réels (20 min)

### Exercice 1 : Coût de Semences
**Contexte Réel :** Au Cameroun, un agriculteur calcule le coût de semences pour une parcelle de maïs.

- Déclarez `quantite_sacs` (int), `prix_sac` (float), `culture` (str).
- Calculez le total (`quantite_sacs * prix_sac`).
- Affichez un message formaté : "Le coût pour X sacs de semences de Y est Z FCFA."

```python
quantite_sacs = 5
prix_sac = 15000.50
culture = "maïs"
# Votre code ici...
```

### Exercice 2 : Conversion de Unités
- Convertissez une surface en hectares (float) en m² (int).
- Gérez une erreur si la surface est négative.

---

## 2. Conditions et Logique : Éligibilité à l'Aide Sociale (20 min)

### Exercice 3 : Vérification d'Éligibilité
**Contexte Réel :** Vérifiez l'éligibilité à une aide sociale basée sur le revenu, le nombre d'enfants et le statut (rural/urbain).

- Si `revenu < 100000` FCFA **ET** `nb_enfants > 2` **OU** `est_rural`, affichez "Éligible à l'aide".
- Sinon, "Non éligible".

```python
revenu_mensuel = float(input("Revenu mensuel (FCFA) : "))
nb_enfants = int(input("Nombre d'enfants : "))
est_rural = input("Zone rurale ? (oui/non) ") == "oui"
# Votre code ici...
```

---

## 3. Boucles : Suivi de Récoltes Journalières (30 min)

### Exercice 5 : Suivi Quotidien
**Contexte Réel :** Suivi de récolte sur 7 jours avec alertes.

- Utilisez `for` avec `range(1, 8)`.
- Générez un rendement aléatoire (`random.randint(50, 200)` kg/jour).
- Si `rendement < 100`, passez au suivant (`continue`).
- Si `rendement < 50`, arrêtez tout (`break`) avec une alerte.

---

## 4. Fonctions : Outil de Budget Familial (30 min)

### Exercice 7 : Calcul Budget
**Contexte Réel :** Calcul de budget mensuel (Nourriture, Transport, Éducation).

- Définissez `calculer_budget(nourriture, transport, *autres)`.
- Retournez la somme totale.

---

## 5. Structures de Données : Gestion d'Inventaire (30 min)

### Exercice 9 : Liste et Dictionnaire
- Créez une liste de médicaments.
- Créez un dictionnaire pour les détails d'un médicament (nom, prix, quantité).

---

## 🏆 Projet Intégrateur : Système de Gestion de Récoltes (30 min)

**Scénario :** Un agriculteur suit les récoltes de cacao sur 5 jours, calcule la moyenne, identifie les jours faibles (< 100kg), et stocke tout dans un dictionnaire.

---

## 🚀 Procédure de Soumission (Git)

1. **Cloner le dépôt :**
   `git clone https://github.com/club-genie-informatique-enspy/TP-PYTHON-TRAINING.git`
2. **Créer une branche :**
   `git checkout -b tp_python/tp1-<votre-nom>-<votre-prenom>`
3. **Commiter :**
   `git commit -m "tp_python(tp1): ajout systeme gestion recoltes"`
4. **Push & PR :**
   Envoyez vers GitHub et créez une **Pull Request** vers `main`.
