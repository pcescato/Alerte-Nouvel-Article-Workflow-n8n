[![n8n](https://img.shields.io/badge/n8n-automation-blue.svg)](https://n8n.io)
[![OpenRouter](https://img.shields.io/badge/OpenRouter-AI_API-orange)](https://openrouter.ai/)

Lang: French 🇫🇷
Made with ❤️ by @pcescato

🔗 Ce code a servi d'exemple dans l'article [n8n – l'interface ultime pour l'automatisation](https://zone-test.ovh/n8n-interface-ultime-automatisation/)

# 📬 Alerte Nouvel Article – Workflow n8n

<img width="817" height="702" alt="image" src="https://github.com/user-attachments/assets/8bc39384-1687-47bc-988d-8bfa090aa57e" />


Ce workflow `n8n` permet d'envoyer automatiquement une notification par email aux abonnés (rôle `subscriber`) lorsqu’un nouvel article est publié sur un site WordPress. Il est conçu pour s’intégrer avec WP Webhooks et utilise un modèle LLM pour générer une accroche personnalisée.

## 🚀 Fonctionnement

1. **Webhook** (POST) reçoit les données de l’article publié depuis WordPress.
2. **Get Users** récupère la liste des utilisateurs via l’API WordPress.
3. **Filter Subscribers** isole les utilisateurs avec le rôle `subscriber` et extrait leur email + nom.
4. **If Subscribers Exist** vérifie s’il y a au moins un abonné.
5. **Prepare Fields** assemble les champs nécessaires pour la suite (titre, contenu, lien, etc.).
6. **Generate Hook** génère une accroche en français à l’aide d’un modèle LLM (OpenRouter, MoonshotAI Kimi K2).
7. **Build Email Payloads** construit un tableau d’emails à envoyer, avec accroche incluse.
8. **Send Email** envoie un email HTML à chaque abonné.

## 🧠 Technologies utilisées

- [n8n](https://n8n.io/) (automatisation)
- API WordPress (authentification requise)
- [OpenRouter](https://openrouter.ai/) (pour accéder à un LLM, ici Kimi)
- SMTP (paramétrable dans n8n)

## 📦 Dépendances

- Connexion API WordPress avec accès à `/wp/v2/users`
- Compte OpenRouter avec un modèle configuré (ou autre LLM compatible)
- Accès SMTP (configuré dans les credentials n8n)
- Webhook côté WordPress (via plugin [WP Webhooks](https://wp-webhooks.com/))

## 🛡️ Sécurité & anonymisation

Cette version publique :
- **Supprime** tous les identifiants sensibles (`webhookId`, `credentials.id`, etc.)
- **Masque** l’adresse email d’envoi par défaut (`example@example.com`)
- Est conçue pour être **configurable** facilement dans une instance n8n personnelle

## 🔧 Personnalisation

Tu peux adapter :
- Le style du prompt génératif dans le nœud "Generate Hook"
- Le contenu HTML dans le nœud "Send Email"
- Le filtre des rôles (actuellement `subscriber`)
- Le modèle utilisé dans le nœud "LLM Model"

## 📤 Déploiement

1. Importer le fichier JSON dans n8n
2. Configurer les **credentials** :
   - API WordPress
   - OpenRouter ou autre fournisseur de LLM
   - Compte SMTP
3. Relier le webhook à WP Webhooks (`POST` vers `/webhook/new-article`)

## 📄 Licence

Apache 2

---

> ✉️ Ce workflow a été conçu pour simplifier la notification éditoriale tout en explorant le potentiel des modèles de langage pour la génération de contenus courts et engageants.
