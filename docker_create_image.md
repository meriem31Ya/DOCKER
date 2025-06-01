# 🐳 TP Docker 1 — Récupérer et lancer des conteneurs

## 🎯 Objectif du TP

Tu dois :

- Récupérer deux images officielles depuis Docker Hub :
  - **MySQL**
  - **PHP 8 avec Apache**
- Lancer un conteneur à partir de chacune de ces images
- Vérifier qu’ils fonctionnent

---

## 🔍 Docker Hub

➡️ Va sur [https://hub.docker.com/](https://hub.docker.com/) et cherche les images suivantes :

- `mysql`
- `php:8.0-apache`

Lis bien la documentation de chaque image officielle pour comprendre les variables d’environnement et les options disponibles.

---

## ✅ Étapes à suivre

### 1. Vérifie que Docker est installé

```bash
docker --version
```

Puis teste avec :

```bash
docker run hello-world
```

---

### 2. Récupère les images Docker officielles (exemple)

#### 📦 MySQL

```bash
docker pull mysql
```

#### 📦 PHP 8 avec Apache

```bash
docker pull php:8.0-apache
```

---

### 3. Lance les conteneurs

#### 🚀 Lancer un conteneur MySQL

```bash
docker run --name mon-mysql -e MYSQL_ROOT_PASSWORD=1234 -d mysql
```

> ✅ `MYSQL_ROOT_PASSWORD` permet de définir le mot de passe du compte root.

#### 🚀 Lancer un conteneur PHP avec Apache

```bash
docker run --name mon-apache -d -p 8080:80 -v $(pwd):/var/www/html php:8.0-apache
```

> Accède à ton navigateur : http://localhost:8080

---

## 🧪 Vérifications

- Liste les conteneurs en cours d’exécution :

```bash
docker ps
```

- Liste les images présentes sur ta machine :

```bash
docker images
```

## 🧽 Nettoyage (optionnel)

Arrêter les conteneurs :

```bash
docker stop mon-mysql mon-apache
```

Supprimer les conteneurs :

```bash
docker rm mon-mysql mon-apache
```

---

> Bravo, tu viens d’exécuter ton premier environnement de développement conteneurisé ! 🎉
