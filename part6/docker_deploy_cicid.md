# 🚀 Déploiement CI/CD d’un Projet PHP Dockerisé avec GitLab

## 🧱 Organisation des branches Git

| Branche   | Rôle                                      |
| --------- | ----------------------------------------- |
| `dev`     | Développement local                       |
| `staging` | Intégration continue : tests, build, scan |
| `preprod` | Tests utilisateurs réalistes              |
| `main`    | Déploiement automatique sur serveur       |
| `prod`    | Déploiement manuel validé                 |

---

## 🔄 Workflow par environnement

### 🔧 `dev`

- Développement local
- Build et tests manuels

### 🧪 `staging`

- Merge des PR
- Pipeline CI : tests, build, scan sécurité
- Aucun déploiement

### 🧷 `preprod`

- Tests utilisateurs en conditions proches de la prod
- Déploiement manuel ou semi-automatisé

### 🚀 `main`

- CI complète + déploiement automatique sur le serveur
- Notification de succès ou d’échec

### 📦 `prod`

- Déploiement manuel après validation finale

---

## ⚙️ dans un premier vous allez pouvoir deployer directement sur la branche main

🔐 N'oubliez pas d'ajouter la clé `SSH_PRIVATE_KEY` dans les variables d’environnement du projet en cours (section CI/CD ou équivalent selon la plateforme utilisée).

> Ce fichier permet d’exécuter un pipeline CI/CD dans GitLab, avec transfert des fichiers vers un serveur distant et relance de `docker-compose`.

```yaml
image: alpine:latest # Image de base légère

stages:
  - deploy # Étape de déploiement sur le VPS

variables:
  DEPLOY_USER: # Utilisateur SSH
  DEPLOY_HOST: # IP du VPS distant
  DEPLOY_PATH: # Chemin distant du projet
  SSH_KEY_PATH: # Chemin temporaire de la clé SSH

deploy_prod:
  stage: deploy
  only:
    - main # Ce job ne s'exécute que sur la branche `main`

  before_script:
    # 📦 Installation des outils nécessaires (SSH et rsync)
    -

    # 🧬 Création du fichier contenant la clé privée à partir de la variable d’environnement
    - echo "$SSH_PRIVATE_KEY" > $SSH_KEY_PATH
    - chmod 600 $SSH_KEY_PATH              # 🔐 Droits sécurisés pour la clé SSH

    # 🔄 Démarrage de l'agent SSH et ajout de la clé
    - eval $(ssh-agent -s)
    - ssh-add $SSH_KEY_PATH

    # 🛡️ Ajout de l’empreinte SSH du serveur à known_hosts pour éviter la demande de confirmation
    - mkdir -p ~/.ssh
    - ssh-keyscan -H $DEPLOY_HOST >> ~/.ssh/known_hosts

  script:
    # 📤 Transfert des fichiers depuis le dépôt GitLab vers le serveur
    - echo "📦 Transfert des fichiers vers le VPS..."
    -

    # 🚀 Connexion au serveur en SSH, arrêt des conteneurs existants, rebuild et relance
    - echo "🚀 Déploiement Docker sur le VPS..."
    -
      "
```

## ⚙️ Dans un deuxième temps vous allez pouvoir rajouter un stage test avant la partie deploy
