# 🎓 TP 3 - Mois 3 : Python Avancé et Asynchronisme (Examen Complet)

## 🎯 Objectifs du TP (3h)

Ce TP évalue votre maîtrise des concepts avancés de Python nécessaires pour le développement de systèmes haute performance et la gestion de projets professionnels.

---

## 1. Décorateurs et Closures : Sécurité et Performance (45 min)
**Scénario :** Vous travaillez pour une startup de Fintech à Douala.

- Créez une closure `generer_id_transaction(prefixe)` qui retourne une fonction générant des IDs successifs (ex: TX-1, TX-2).
- Créez un décorateur `@verifier_admin` qui vérifie si une variable globale `est_admin` est à `True`.
- Créez un décorateur `@timeout(secondes)` qui avertit si une fonction dépasse un délai.

```python
# Exemple de base
est_admin = False

def verifier_admin(fonction):
    # Votre code ici...
```

---

## 2. Programmation Asynchrone : Scraper de Prix (1h)
**Scénario :** Simulez la récupération de prix de cacao depuis 3 marchés en parallèle.

- Utilisez `asyncio` et `async/await`.
- Utilisez `asyncio.gather` pour la simultanéité.
- Gérez les échecs avec `try/except` (simulez 50% d'erreurs).

---

## 3. Outillage Avancé : Logging et Configuration (30 min)
- Configurez un `logger` vers `errors.log` et la console.
- Chargez vos constantes (URL, tentatives) depuis un fichier `.env`.
- Logguez les erreurs fatales via `sys.excepthook`.

---

## 4. Multi-threading : Traitement de Données (45 min)
- Utilisez `ThreadPoolExecutor` pour simuler le traitement de plusieurs tâches I/O-bound.
- Comparez le gain de temps par rapport au mode séquentiel.

---

## 🏆 Projet Final : Micro-Service de Monitoring (1h)
**Consigne :**
Créez un script complet unifiant les concepts :
1. Configuration par `.env`.
2. Décorateurs de logs et chrono.
3. Vérification asynchrone d'URLs.
4. Rapport final dans un fichier log.

---

## 🚀 Procédure de Soumission (Git)

1. **Cloner le dépôt :**
   `git clone https://github.com/club-genie-informatique-enspy/TP-PYTHON-TRAINING.git`
2. **Créer une branche :**
   `git checkout -b tp_python/tp3-<votre-nom>-<votre-prenom>`
3. **Commiter :**
   `git commit -m "tp_python(tp3): ajout micro-service monitoring et deco"`
4. **Push & PR :**
   Envoyez vers GitHub et créez une **Pull Request** vers `main`.
