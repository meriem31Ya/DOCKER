# 🚀 Déploiement CI/CD pour projet Dockerisé

## 🧱 Organisation des branches

| Branche   | Rôle                                        |
| --------- | ------------------------------------------- |
| `main`    | Branche stable avec déploiement automatique |
| `dev`     | Développement actif                         |
| `staging` | Tests d'intégration                         |
| `preprod` | Réplique de prod pour vérification finale   |
| `prod`    | Déploiement manuel validé                   |

---

## ⚙️ CI/CD sur `main`

1. Push sur `main`
2. Le pipeline CI exécute :
   - Build de l’image Docker
   - Tests (PHPUnit, lint, etc.)
   - Push vers Docker Hub ou GitLab Registry
   - Déploiement automatique sur VPS / Cloud
3. Notification de succès ou échec

---

## 📂 Exemple de `.dockerignore`

```txt
.git
tests
node_modules
vendor
*.log
.env
Dockerfile
docker-compose.yml
```

---

## 🔁 Workflow par environnement

### `dev`

- Développement en local
- Build manuel

### `staging`

- Merge des PR
- CI : tests, build, scan sécurité
- Déploiement automatique

### `preprod`

- Tests utilisateurs avec données proches de prod
- Déploiement manuel ou semi-automatisé

### `prod`

- Déploiement manuel validé

---

## 📦 Bonnes pratiques

- Utiliser `.dockerignore` pour alléger l’image
- Versionner les images avec des tags dynamiques
- Ne jamais stocker de secrets ou `.env` dans le repo
- Tester les images localement avant push
- Documenter chaque étape dans le README

---

## 🔄 Pipeline avec Docker Hub

### Clonage et authentification Docker

```yaml
before_script:
  - echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin

script:
  - docker pull votre_identifiant_docker/votre_image:latest
```

---

## ⚡ Déploiement avec Resync

1. Installer Resync sur local et VPS
2. Créer le fichier `.resync.yml` :

```yml
sync:
  - source: .
    target: user@votre-ip:/home/user/app
    exclude:
      - .git
      - node_modules
      - vendor
      - .dockerignore
```

3. Lancer la synchronisation :

```bash
resync up
```

---

## 🚫 Fichiers à ignorer

À ajouter dans `.dockerignore` **et** `.resync.yml` :

```txt
.git
node_modules
vendor
.dockerignore
.docker-compose.override.yml
.env
```
