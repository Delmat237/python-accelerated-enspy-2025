# 🛠️ MOIS 1 / SEMAINE 1 : Syntaxe et Types - L'Atelier de Codage

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Setup** | Démarrer un projet Python de zéro (incluant `venv`). | Configuration professionnelle de l'environnement. |
| **Code-First** | Implémenter un script de conversion monétaire ou de temps. | Maîtrise des types (`int`/`float`) et des opérateurs. |
| **Logique** | Écrire une fonction de vérification d'accès sécurisé. | Utilisation idiomatique de `if/elif/else` et des booléens. |

-----

## 1\. 🚀 Démarrage et Environnement (30 min)

### Défi 1 : La Mise en Place du Chantier

**Objectif :** Créer un environnement isolé et respecter la norme de codage dès le départ.

#### Étapes (À exécuter directement)

1.  Ouvrez votre terminal et créez votre dossier de travail : `mkdir Mois1_Pratique && cd Mois1_Pratique`.
2.  Créez l'environnement virtuel et activez-le : `python -m venv .venv` suivi de `source .venv/bin/activate`.
3.  Créez le premier fichier : `touch semaine1_script.py`.
4.  Dans ce fichier, définissez une variable en respectant **PEP 8 (snake\_case)** :
    ```python
    # Nom de variable conforme : 
    nom_du_projet_final = "Simulateur Bourse"

    # Nom de variable NON conforme :
    # NomDuProjetFinal = "..." 
    ```

#### 💡 Théorie Brève : Le "Pourquoi" du `venv`

L'environnement virtuel garantit la **reproductibilité**. Chaque projet utilise ses propres dépendances, évitant les conflits globaux. C'est la première étape vers l'industrialisation.

-----

## 2\. 🧮 Types de Données et Opérateurs (60 min)

### Défi 2 : Le Convertisseur Intelligent

**Objectif :** Écrire un script qui convertit une durée totale en secondes en un format `H:M:S` et qui utilise le formatage **`f-string`**.

#### 📝 Code Guidé : La Solution

Nous devons utiliser les opérateurs **`//` (division entière)** et **`%` (modulo)** pour isoler les minutes et les secondes.

```python
# 1. Donnée d'entrée (à changer par l'utilisateur)
duree_totale_secondes = 9876 

# 2. Calcul des Heures, Minutes, Secondes restantes
heures = duree_totale_secondes // 3600  # Combien de blocs de 3600s ?
secondes_restantes = duree_totale_secondes % 3600

minutes = secondes_restantes // 60      # Combien de blocs de 60s ?
secondes = secondes_restantes % 60

# 3. Affichage professionnel (F-string)
print(f"Durée totale : {heures}h {minutes}m {secondes}s")

# Défi d'extension : afficher le résultat en un seul appel print() en ligne
# print("Résultat : " + str(heures) + "h " + str(minutes) + "m " + str(secondes) + "s") # À éviter !
```

#### 💡 Théorie Brève : `str` vs. `int` (Immutabilité)

  * Les types **`int`** et **`float`** sont utilisés pour le calcul.
  * Les **`str`** sont pour l'affichage et sont **immutables** (on ne peut pas modifier un caractère sans recréer la chaîne entière). Les `f-strings` simplifient la conversion implicite des types numériques en chaînes.

-----

## 3\. 🚦 Logique Conditionnelle (60 min)

### Défi 3 : Le Garde d'Accès Sécurisé

**Objectif :** Écrire un script qui vérifie si un utilisateur a le droit d'accéder à un système basé sur deux conditions : son statut (Admin ou Utilisateur) et s'il a payé sa licence.

#### 📝 Code Guidé : La Solution `if/elif`

```python
# Variables d'entrée (à manipuler)
statut = "Admin"
licence_active = False
niveau_securite = 4 

# Logique de la porte d'accès
if statut == "Admin" and niveau_securite >= 5:
    # Condition très stricte pour les administrateurs
    print("✅ ACCÈS ADMINISTRATEUR PREMIUM. Bienvenue dans le back-office.")

elif statut == "Admin" and niveau_securite < 5:
    print("⚠️ ACCÈS ADMINISTRATEUR standard. Certains services sont limités.")

elif statut == "Utilisateur" and licence_active:
    # Un utilisateur simple doit avoir une licence active
    print("🔑 ACCÈS UTILISATEUR. Accès aux fonctionnalités de base.")
    
elif not licence_active: 
    # Utilisation de l'opérateur 'not' pour vérifier l'état False
    print("❌ ACCÈS REFUSÉ. Votre licence est inactive.")

else:
    # Cas par défaut si aucune condition ci-dessus n'est remplie
    print("Erreur de statut ou accès non autorisé.")
```

### 🧪 TP EXPRESS : Calculateur de Taux de Remise (15 min)

**Consigne :** Créez une variable `montant_total` et une variable `client_fidele` (`True`/`False`).

1.  Si le montant est supérieur à 1000 € **OU** que le client est fidèle, appliquez une remise de 10%.
2.  Sinon, n'appliquez aucune remise.
3.  Affichez le prix final.

-----

## ⏳ Conclusion de Session (15 min)

  * **Revue de Code :** Correction rapide du TP et discussion sur l'utilisation des parenthèses dans les conditions complexes.
  * **Préparation S2 :** Lecture préparatoire sur les **Listes** et les **Boucles**. Le codage de la semaine prochaine sera orienté vers l'automatisation.

Cette session est conçue pour que les étudiants passent la majorité du temps à taper du code, validant immédiatement la syntaxe et la logique par l'exemple.