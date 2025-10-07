# 🛠️ MOIS_1_FONDATIONS/INSTALLATION_PREREQUIS.md : Prérequis et Installation

## 🎯 Objectifs

Ce guide vous aide à configurer votre environnement de développement pour suivre le programme Python Accéléré. Nous couvrons les prérequis, les IDE recommandés, l'installation de Python sur Windows et Ubuntu, ainsi que la création et l'activation d'environnements virtuels.

-----

## 1\. 📋 Prérequis

Avant de commencer, assurez-vous d'avoir :
- Un ordinateur avec **Windows 10/11** ou **Ubuntu 20.04/22.04** (ou une distribution Linux équivalente).
- Une connexion Internet stable pour télécharger les logiciels.
- Les droits d'administration pour installer des logiciels (si nécessaire).

-----

## 2\. 💻 IDE Recommandés

Un environnement de développement intégré (IDE) facilite l'écriture et le débogage du code. Voici les options populaires :
- **Visual Studio Code (VSCode)** : Recommandé pour ce programme (léger, personnalisable, support Python natif).
- **PyCharm** : Idéal pour les projets complexes (version Community gratuite disponible).
- **Jupyter Notebook** : Parfait pour l'exploration de données (utilisé dans Mois 6).
- **Thonny** : Simple, adapté aux débutants.

Nous utiliserons **VSCode** comme IDE principal dans ce guide.

-----

## 3\. 🐍 Installation de Python

### Sur Windows
1. Téléchargez la dernière version de Python (recommandé : 3.11 ou supérieur) depuis [python.org](https://www.python.org/downloads/).
2. Lancez l'installeur et cochez **"Add Python to PATH"**.
3. Suivez les instructions, choisissez "Install Now", et laissez les paramètres par défaut.
4. Vérifiez l'installation en ouvrant une invite de commande (`cmd`) et en tapant :
   ```bash
   python --version
   ```
   Vous devriez voir quelque chose comme `Python 3.11.5`.

### Sur Ubuntu
1. Mettez à jour les paquets :
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
2. Installez Python et les outils de développement :
   ```bash
   sudo apt install python3 python3-pip python3-venv -y
   ```
3. Vérifiez l'installation dans un terminal :
   ```bash
   python3 --version
   ```
   Résultat attendu : `Python 3.11.x`.

-----

## 4\. 🌐 Création et Activation d'un Environnement Virtuel

Les environnements virtuels isolent les dépendances par projet, une pratique essentielle pour la reproductibilité.

### Sur Windows
1. Créez un dossier pour votre projet (ex: `MOIS_1_FONDATIONS`) :
   ```bash
   mkdir MOIS_1_FONDATIONS
   cd MOIS_1_FONDATIONS
   ```
2. Créez un environnement virtuel :
   ```bash
   python -m venv .venv
   ```
3. Activez-le :
   ```bash
   .venv\Scripts\activate
   ```
   Vous verrez `(.venv)` apparaître avant votre invite de commande.

### Sur Ubuntu
1. Créez un dossier pour votre projet :
   ```bash
   mkdir MOIS_1_FONDATIONS
   cd MOIS_1_FONDATIONS
   ```
2. Créez un environnement virtuel :
   ```bash
   python3 -m venv .venv
   ```
3. Activez-le :
   ```bash
   source .venv/bin/activate
   ```
   Vous verrez `(.venv)` avant votre invite de commande.

-----

## 5\. ⚙️ Configuration de VSCode
1. Téléchargez et installez VSCode depuis [code.visualstudio.com](https://code.visualstudio.com/).
2. Installez l'extension **Python** (par Microsoft) via l'onglet Extensions.
3. Ouvrez le dossier `MOIS_1_FONDATIONS` dans VSCode.
4. Sélectionnez l'interpréteur Python de l'environnement virtuel :
   - Appuyez sur `Ctrl+Shift+P` (ou `Cmd+Shift+P` sur Mac).
   - Tapez "Python: Select Interpreter" et choisissez `./.venv/bin/python` (Ubuntu) ou `./.venv/Scripts/python.exe` (Windows).
5. Créez un fichier `.vscode/settings.json` avec :
   ```json
   {
       "python.linting.enabled": true,
       "python.linting.pylintEnabled": true,
       "python.formatting.provider": "black"
   }
   ```
   Cela active la vérification PEP 8 et le formatage automatique.

-----

## 6\. 📦 Installation des Dépendances
1. Créez un fichier `requirements.txt` dans `MOIS_1_FONDATIONS` avec :
   ```
   pytest
   ```
2. Installez les dépendances dans l'environnement virtuel :
   - Sur Windows : `pip install -r requirements.txt`
   - Sur Ubuntu : `pip3 install -r requirements.txt`
3. Vérifiez l'installation avec :
   ```bash
   pip list
   ```
   Vous devriez voir `pytest` dans la liste.

-----

## ⏳ Conclusion
Vous êtes maintenant prêt à coder ! Testez votre configuration en créant un fichier `test.py` avec :
```python
print("Environnement prêt !")
```
Exécutez-le avec `python test.py` (Windows) ou `python3 test.py` (Ubuntu). Pour désactiver l'environnement virtuel, utilisez `deactivate` sur les deux systèmes.

**Préparation S1 :** Consultez `SEMAINE_1_Syntaxe_Types.md` pour débuter avec la syntaxe Python.

