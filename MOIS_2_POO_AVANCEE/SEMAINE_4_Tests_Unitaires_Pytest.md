# MOIS_2_POO_AVANCEE/SEMAINE_4_Tests_Unitaires_Pytest.md : SEMAINE 4 : Tests Unitaires avec Pytest

## Objectifs Pédagogiques (3h)

| Objectif | Pourquoi c’est crucial ? |
|---------|--------------------------|
| **Comprendre les Tests Unitaires** | Vérifier que chaque petit bloc de code fonctionne isolément. |
| **Utiliser `pytest`** | Automatiser la vérification de vos classes de façon professionnelle. |
| **La Méthode AAA** | Organiser ses tests de manière lisible et standardisée. |
| **Faire du TDD (Test Driven Development)** | Écrire le test *avant* le code pour une meilleure conception. |

---

## 1. Pourquoi Tester ? (30 min)

Les tests garantissent que vos modifications n'ont pas cassé de fonctionnalités existantes (non-régression). Ils servent aussi de documentation vivante.

> [!IMPORTANT]
> **Deep Dive : Le Pattern AAA (Arrange, Act, Assert)**
> Tous les bons tests suivent cet ordre :
> 1. **Arrange** : On prépare les données (ex: créer un compte avec 100€).
> 2. **Act** : On exécute l'action à tester (ex: retirer 50€).
> 3. **Assert** : On vérifie le résultat (ex: le solde est-il bien à 50€ ?).

---

## 2. Tester nos Classes avec Pytest (1h30)

### Défi 1 : Ma première Fixture

Une **fixture** est une fonction qui prépare un objet pour plusieurs tests.

```python
import pytest
from compte_bancaire import CompteBancaire

@pytest.fixture
def compte_vide():
    return CompteBancaire("Testeur", 0)

def test_depot_valide(compte_vide):
    # Act
    compte_vide.deposer(500)
    # Assert
    assert compte_vide.solde == 500
```

> [!TIP]
> **Pro Tip : La Paramétrisation**  
> Au lieu d'écrire 5 tests pour tester 5 montants différents, utilisez `@pytest.mark.parametrize`.  
> Cela permet de lancer le même test avec une liste de valeurs d'entrée et de résultats attendus.

---

## 3. Tester les Erreurs (30 min)

Il est tout aussi important de tester que votre code *échoue* quand il le doit.

#### 📝 Code Guidé : `pytest.raises`

```python
def test_retrait_trop_eleve(compte_vide):
    with pytest.raises(ValueError, match="Montant positif requis"):
        compte_vide.deposer(-10)
```

---

## 4. TP Intégrateur : Couverture Totale (1h)

**Objectif :** Atteindre 100% de couverture sur la classe `CompteEpargne`.

> [!WARNING]
> **Piège Courant : Les Effets de Bord**  
> Si votre test crée un fichier sur le disque, assurez-vous qu'il le supprime après (ou utilisez les fixtures `tmp_path` de Pytest). Un test ne doit jamais laisser de "saleté" derrière lui, sinon les tests suivants risquent d'échouer à cause de lui.

---

## 🧪 TP SUPPLÉMENTAIRES (Pour aller plus loin)

### Exercice 1 : Test de la Calculatrice
Reprenez votre fonction `calculer_moyenne` de la Semaine 2.
Écrivez des tests pour :
1. Une liste de notes normale.
2. Une liste vide (doit retourner 0 ou lever une erreur selon votre choix).
3. Une note négative.

### Exercice 2 : Fixture de Zoo
Créez une fixture `zoo_peuple` qui retourne une liste contenant un `Chien` et un `Chat`.
Testez que la méthode `faire_aboyer_tout_le_monde` fonctionne correctement sur cette fixture.

---

## ⏳ Conclusion du Mois 2

Félicitations ! Vous avez transformé votre façon de coder : de simples scripts à un **système orienté objet complet, sécurisé et testé**.

  * **Revue :** Pourquoi dit-on que les tests sont un investissement ? (On gagne du temps sur le long terme en évitant les bugs répétitifs).
  * **Prochaine Étape :** Le Mois 3 portera sur les Bases de Données (SQL) pour persister vos objets !
