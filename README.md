# 🚀 Python Accéléré (L1 – L3) – Programme Intensif 6 Mois

Bienvenue dans le dépôt officiel de la formation Python Accéléré Club GI-ENSPY (2025-2026).
Ce programme vous guide du fondamental au déploiement, en 6 mois intensifs, structurés comme un vrai parcours d’ingénieur logiciel 🧠💻.


-----

## 📑 Sommaire

- [🚀 Python Accéléré (L1 – L3) – Programme Intensif 6 Mois](#-python-accéléré-l1--l3--programme-intensif-6-mois)
  - [📑 Sommaire](#-sommaire)
  - [🧭 Objectifs](#-objectifs)
  - [🗓️ Roadmap 6 Mois](#️-roadmap-6-mois)
  - [🧱 Structure du Dépôt](#-structure-du-dépôt)
  - [🛠️ Installation \& Configuration](#️-installation--configuration)
    - [1. Cloner le dépôt](#1-cloner-le-dépôt)
    - [2. Créer et activer un environnement virtuel](#2-créer-et-activer-un-environnement-virtuel)
    - [3. Installer les dépendances communes](#3-installer-les-dépendances-communes)
  - [🧪 Validation Professionnelle](#-validation-professionnelle)
  - [📎 Ressources Utiles](#-ressources-utiles)
  - [🧠 Inspiré de](#-inspiré-de)
  - [🧑‍🏫 Crédits](#-crédits)
  - [📝 Licence](#-licence)

-----

## 🧭 Objectifs

  - Maîtriser la syntaxe et la logique Python moderne.
  - Construire des API performantes avec **FastAPI** et des apps web avec **Django**.
  - Explorer les bases de la **Data Science** (NumPy, Pandas, scikit-learn).
  - Déployer des applications conteneurisées avec **Docker** et CI/CD.
  - Constituer un **portfolio GitHub** professionnel validé par code review.

-----

## 🗓️ Roadmap 6 Mois

| Mois | Module Principal             | Focus                                | Projet Fil Rouge                       |
|------|-------------------------------|---------------------------------------|-----------------------------------------|
| 1    | Fondations & Algorithmique    | Syntaxe, Structures, Fonctions, I/O  | 📝 Simulateur de Bourse                |
| 2    | POO & Architecture            | Héritage, Tests Unitaires            | 🏦 Système de Gestion Bancaire        |
| 3    | Python Avancé & Asynchrone    | Décorateurs, Asyncio, Threads        | 🕸️ Scraper Web Asynchrone            |
| 4    | APIs Haute Performance        | FastAPI, JWT, PostgreSQL             | 🧩 Microservices REST                 |
| 5    | Full-Stack Django             | ORM, DRF, MVT                        | 📰 Blog / Forum Complet               |
| 6    | Data & DevOps                 | Pandas, ML, Docker, CI/CD            | 🚢 Application Déployée en Production |

> 📚 Structure détaillée extraite de la [roadmap officielle](https://www.google.com/search?q=./roadmap_python.pdf), débutée le 28 juillet 2025.

-----

## 🧱 Structure du Dépôt

```bash
.
├── .github/
│   └── workflows/
│       └── ci_cd_pipeline.yml            # Scripts CI/CD pour le Mois 6
├── INTRODUCTION.md                       # Chapitre d'introduction (Historique, PEP)
├── README.md
├── LICENSE
├── requirements.txt                      # Dépendances générales (pytest)
├── roadmap_python.pdf
│
├── MOIS_1_FONDATIONS/                    # (Semaines 1 à 4 : Logique Algorithmique)
│   ├── INSTALLATION_PREREQUIS.md #  Prérequis et Installation
│   ├── SEMAINE_1_Syntaxe_Types.md        # Types de base, if/elif/else, PEP 8
│   ├── SEMAINE_2_Boucles_Fonctions.md    # for/while, def, *args, Scope
│   ├── SEMAINE_3_Structures_Donnees.md   # list, dict, tuple, Compréhensions
│   ├── SEMAINE_4_IO_Robustesse_Projet.md # with open, try/except, Module random
│   ├── TP1.md                            # Examen Final Mois 1 (FR)
│   ├── TP1_EN.md                         # Month 1 Final Exam (EN)
│   └── TP_Simulateur_Bourse/
│       └── simulateur.py
│
├── MOIS_2_POO_AVANCEE/                   # (Semaines 1 à 4 : POO & Qualité)
│   ├── SEMAINE_1_Classes_Encapsulation.md # class, __init__, @property, setters
│   ├── SEMAINE_2_Heritage_Polymorphisme.md # super(), Dunder Methods (__str__)
│   ├── SEMAINE_3_Methodes_Classe_Statiques.md # @classmethod, @staticmethod, Factory
│   ├── SEMAINE_4_Tests_Unitaires_Pytest.md # Installation de pytest, assert, pytest.raises
│   ├── TP2.md                            # Examen Final Mois 2 (FR)
│   ├── TP2_EN.md                         # Month 1 Final Exam (EN)
│   ├── cours_poo_avance.tex                # Le cours théorique (LaTeX)
│   ├── tests/
│   │   └── test_systeme_bancaire.py        # Suite de tests Pytest (Livrable S4)
│   └── TP_Systeme_Bancaire/
│       └── compte_bancaire.py
│
├── MOIS_3_ASYNCHRONE_OUTILLAGE/          # (Semaines 1 à 4 : Avancé & Asynchrone)
│   ├── SEMAINE_1_Decorateurs.md          # Décorateurs, closures
│   ├── SEMAINE_2_Asyncio_Threads.md      # Asyncio, threading
│   ├── SEMAINE_3_Outillage_Avance.md     # Gestion erreurs, logging
│   ├── SEMAINE_4_Scraper_Projet.md       # Projet scraper asynchrone
│   ├── TP3.md                            # Examen Final Mois 3 (FR)
│   ├── TP3_EN.md                         # Month 3 Final Exam (EN)
│   └── Projet_Scraper/
│       └── scraper_async.py
│
├── MOIS_4_API_FASTAPI/                   # (Semaines 1 à 4 : FastAPI)
│   ├── SEMAINE_1_Fondamentaux_FastAPI.md # Type hints, Pydantic
│   ├── SEMAINE_2_Auth_JWT.md             # Authentification JWT
│   ├── SEMAINE_3_PostgreSQL.md           # Intégration bases de données
│   ├── SEMAINE_4_Microservices.md        # Projet microservices
│   ├── main.py
│   ├── models.py
│   └── Projet_Microservice/
│
├── MOIS_5_DJANGO_FULLSTACK/              # (Semaines 1 à 4 : Django)
│   ├── SEMAINE_1_Architecture_MVT.md     # Modèles, vues, templates
│   ├── SEMAINE_2_ORM_DRF.md              # ORM, Django REST Framework
│   ├── SEMAINE_3_Formulaires.md          # Formulaires, validation
│   ├── SEMAINE_4_Blog_Projet.md          # Projet blog/forum
│   ├── django_app/
│   └── Projet_Blog/
│
└── MOIS_6_DATA_DEVOPS/                   # (Semaines 1 à 4 : Data & DevOps)
    ├── SEMAINE_1_Data_Science.md         # NumPy, Pandas
    ├── SEMAINE_2_Machine_Learning.md     # Scikit-learn
    ├── SEMAINE_3_DevOps_Docker.md        # Docker, CI/CD
    ├── SEMAINE_4_Projet_Final.md         # Déploiement
    ├── notebooks/
    ├── docker/
    └── Projet_Final/
```

-----

## 🛠️ Installation & Configuration

### 1\. Cloner le dépôt

```bash
git clone https://github.com/Delmat237/python-accelerated-enspy-2025.git
cd python-accelerated-enspy-2025
```

### 2\. Créer et activer un environnement virtuel

```bash
python -m venv .venv
source .venv/bin/activate  # macOS/Linux
# ou
.venv\Scripts\activate     # Windows
```

### 3\. Installer les dépendances communes

```bash
pip install -r requirements.txt
```

-----

## 🧪 Validation Professionnelle

| Critère | Description | Pondération |
| :--- | :--- | :--- |
| ✅ Code Review | PEP8, sécurité, structure | 40% |
| 🧰 Portfolio GitHub | Projets documentés & publics | 30% |
| 📝 Examens Blancs | PCEP / PCAP mock exams | 30% |

-----

## 📎 Ressources Utiles

  * [Documentation Python](https://docs.python.org/3/)
  * [FastAPI Docs](https://fastapi.tiangolo.com/)
  * [Django Docs](https://docs.djangoproject.com/)
  * [Python Institute Certifications](https://pythoninstitute.org/)

-----

## 🧠 Inspiré de

  * Coursera Specialization “Python for Everybody”
  * OpenEDG Python Institute (PCEP/PCAP/PCPP)
  * [Roadmap Python Formation ENSPY 2025](https://www.google.com/search?q=./roadmap_python.pdf)

-----

## 🧑‍🏫 Crédits

> Département de Génie Informatique – ENSPY
> Programme 2025-2026 – Club GI ENSPY

-----

## 📝 Licence

Ce projet est distribué sous licence MIT. Voir [LICENSE](https://www.google.com/search?q=./LICENSE).
