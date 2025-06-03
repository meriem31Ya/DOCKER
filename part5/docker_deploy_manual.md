# 🚀 Déployer manuellement un projet Dockerisé sur un serveur VPS

Ce guide te montre **comment déployer un projet Docker (avec Docker Compose)** manuellement sur un **serveur VPS Linux**, de manière sécurisée via SSH.

---

## 🎯 Objectif

- Créer une clé SSH pour se connecter sans mot de passe
- Transférer le code du projet sur le VPS
- Installer Docker et Docker Compose sur le serveur
- Lancer le projet sur le serveur distant

---

## 🛠️ 1. Générer une clé SSH (sur ta machine locale)

```bash
ssh-keygen -t rsa -b 4096 -C "votre_email@example.com"
```

> Appuie sur **Entrée** plusieurs fois pour accepter les valeurs par défaut.

Les fichiers générés :

- `~/.ssh/id_rsa` → clé privée (ne jamais partager)
- `~/.ssh/id_rsa.pub` → clé publique

---

## 📤 2. Ajouter la clé publique sur le serveur

Envoie la clé publique sur ton VPS (remplace `user@ip_vps`) :

```bash
ssh-copy-id user@ip_vps
```

si vous avez plusierus clés:

```bash
ssh-copy-id -i ~/.ssh/nomclé.pub user@ip
```

> Tu peux maintenant te connecter sans mot de passe :

```bash
ssh user@ip_vps
ssh -i ~/.ssh/id_rsa_gitlabci user@ip_vps

```

---

## 🐳 3. Installer Docker & Docker Compose sur le VPS

Une fois connecté au VPS :

### Installer Docker

```bash
curl -fsSL https://get.docker.com | sh
ou
curl -fsSL https://get.docker.com | sudo bash

```

### Ajouter ton utilisateur au groupe docker

```bash
sudo usermod -aG docker $USER
```

> Déconnecte-toi puis reconnecte-toi pour que le changement prenne effet.

### Installer Docker Compose

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/v2.24.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

---

## 🧳 4. Transférer le projet sur le serveur

Depuis ta machine locale :

```bash
scp -i ~/.ssh/cléprivé -r lien du projet-local user@ip:/var/www/
```

---

## 🚀 5. Lancer le projet sur le serveur

Connecte-toi sur le VPS :

```bash
ssh user@ip_vps
cd mon-projet
docker-compose up --build -d
```

---

## 🔍 6. Vérifications

- Accède au projet dans le navigateur : `http://ip_vps:PORT`
- Vérifie les conteneurs :

```bash
docker ps
```

- Voir les logs :

```bash
docker-compose logs
```

---

## 🧽 7. Nettoyage (optionnel)

```bash
docker-compose down -v
```

---

## ✅ Résultat attendu

- Ton projet est lancé en ligne depuis un serveur VPS
- Tu peux y accéder depuis ton navigateur via l’adresse IP publique

---

> Félicitations, tu as déployé un environnement Dockerisé manuellement sur un VPS 🐳🚀
