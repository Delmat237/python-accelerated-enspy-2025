# 🛠️ MOIS 2 / SEMAINE 1 : Classes, Constructeur et Encapsulation

## 🎯 Objectifs de la Session (2h - 2h30)

| Mode | Objectif Pratique | Compétences Validées |
| :--- | :--- | :--- |
| **Modélisation** | Définir la classe de base `CompteBancaire` et son constructeur. | Structuration des données (`__init__`). |
| **Sécurité** | Protéger les attributs cruciaux (ex: `_solde`) contre les modifications directes. | Maîtrise de l'**Encapsulation** (convention `_` et `@property`). |
| **Robustesse** | Implémenter la validation du solde lors du dépôt ou du retrait. | Utilisation du **`@attribut.setter`** pour contrôler l'état interne. |

-----

## 1\. 🧱 Le Pilier I : Définition et Initialisation (45 min)

### Défi 1 : La Carte d'Identité de l'Objet

**Objectif :** Créer la classe `CompteBancaire` et son constructeur (`__init__`) pour initialiser l'état initial du compte.

#### 📝 Code Guidé : Structure de Classe

```python
# Fichier : compte_bancaire.py
class CompteBancaire:
    
    # 1. Attribut de Classe (Partagé par toutes les instances)
    taux_frais_gestion = 0.01 

    def __init__(self, titulaire: str, solde_initial: float = 0.0):
        """
        Constructeur : Initialise les attributs de l'objet. (PEP 257)
        
        Args:
            titulaire (str): Le nom du propriétaire du compte.
            solde_initial (float): Le montant initial sur le compte.
        """
        self.titulaire = titulaire
        
        # 2. Convention d'Encapsulation (Attribut Protégé)
        # Le underscore '_' indique que cet attribut ne doit pas être modifié directement.
        self._solde = solde_initial 
        
        # 3. Validation initiale (Robustesse M1)
        if self._solde < 0:
            raise ValueError("Le solde initial ne peut pas être négatif.")
            
    # Méthode d'instance
    def deposer(self, montant: float):
        if montant <= 0:
            raise ValueError("Le montant du dépôt doit être positif.")
        self._solde += montant
        return f"Dépôt de {montant} effectué. Nouveau solde: {self._solde:.2f}."

# Instanciation (Création d'objets)
compte_alice = CompteBancaire("Alice Dupont", 500.00)
print(compte_alice.deposer(150.00)) 
```

-----

## 2\. 🔒 Le Pilier II : Encapsulation avec `@property` (60 min)

L'Encapsulation est essentielle pour contrôler la lecture et l'écriture des attributs internes. En Python, on utilise les **propriétés** pour transformer une méthode en un attribut contrôlé.

### Défi 2 : Rendre le Solde Lisible (Mais Non Modifiable Directement)

**Objectif :** Créer un *getter* pour le solde. Le développeur doit pouvoir lire `compte.solde`, mais cela appellera la méthode `solde()`, offrant ainsi une couche de contrôle.

#### 📝 Code Guidé : `@property` (Le Getter)

Ajoutez ce bloc à la classe `CompteBancaire` :

```python
# Dans la classe CompteBancaire...

    @property
    def solde(self):
        """
        [GETTER] Permet l'accès en lecture au solde protégé (_solde).
        Accès via : compte.solde
        """
        # On peut mettre ici des règles métier avant de retourner la valeur,
        # par exemple, déduire des frais d'affichage
        print("(Lecture sécurisée du solde)")
        return self._solde
        
# Utilisation
compte_alice = CompteBancaire("Alice Dupont", 500.00)

# ❌ Tenter d'accéder à l'attribut protégé (déconseillé)
# print(compte_alice._solde) 

# ✅ Accès sécurisé via le getter @property
print(f"Le solde actuel est : {compte_alice.solde:.2f}") 
```

-----

## 3\. ⚙️ Retrait et Contrôle d'Écriture (75 min)

Le `setter` est la contrepartie du `getter`. Il est utilisé pour valider les données avant qu'elles n'altèrent l'état de l'objet.

### Défi 3 : Retrait et Validation de l'Opération

**Objectif :** Écrire la méthode `retirer()` qui lève une exception si le retrait dépasse le solde disponible (solde insuffisant).

#### 📝 Code Guidé : Retrait et Logique Métier

Ajoutez la méthode `retirer` à la classe `CompteBancaire` :

```python
# Dans la classe CompteBancaire...

    def retirer(self, montant: float):
        """
        Effectue un retrait après vérification du solde.
        """
        if montant <= 0:
            raise ValueError("Le montant du retrait doit être positif.")
            
        # 1. Logique métier : Vérification du solde
        if montant > self._solde:
            # Lève une exception (M1/S4) si la règle métier est violée
            raise ValueError("Solde insuffisant pour effectuer ce retrait.")
            
        # 2. Opération
        self._solde -= montant
        return f"Retrait de {montant} effectué. Nouveau solde: {self._solde:.2f}."

# Utilisation et test de la robustesse
compte_bob = CompteBancaire("Bob Martin", 100.00)

# Succès
print(compte_bob.retirer(30.00)) # Nouveau solde: 70.00

# Échec (Gestion de l'exception via try/except)
try:
    compte_bob.retirer(200.00) 
except ValueError as e:
    print(f"❌ ERREUR interceptée : {e}")

print(f"Solde final de Bob (lecture via @property) : {compte_bob.solde:.2f}")
```

-----

## ⏳ Conclusion de Session (30 min)

### 🧪 TP EXPRESS : Implémenter un `@solde.setter`

**Consigne :** Ajoutez le *setter* au `solde` dans la classe `CompteBancaire`.

```python
# Dans la classe CompteBancaire...
# ...
    @solde.setter
    def solde(self, nouvelle_valeur):
        """
        [SETTER] Permet le contrôle d'écriture sur le solde.
        """
        if nouvelle_valeur < 0:
            raise ValueError("Le solde ne peut pas être fixé à une valeur négative.")
        self._solde = nouvelle_valeur

# Testez le code :
# compte_alice.solde = 1000  # Devrait fonctionner
# compte_alice.solde = -50   # Devrait lever une ValueError
```

**Prochaine Étape :** La Semaine 2 abordera l'**Héritage** et le **Polymorphisme** pour créer la classe dérivée `CompteÉpargne` et spécialiser son comportement.