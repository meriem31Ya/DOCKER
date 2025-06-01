# 🐳 TP Docker Compose — Lancer un site PHP avec MySQL et phpMyAdmin

Apprends à lancer un environnement web complet (PHP + Apache + MySQL + phpMyAdmin) avec **Docker Compose**.

---

## 🎯 Objectif pédagogique

- Comprendre le rôle de `docker-compose.yml`
- Lancer plusieurs services dans un même environnement
- Configurer un site PHP qui communique avec une base de données MySQL

---

## 📚 Prérequis

- Docker & Docker Compose installés
- Savoir créer un fichier `index.php`
- Savoir lire un `Dockerfile` basique

---

## 📁 Structure de ton projet

```
mon-projet/
├── docker-compose.yml
├── site/
│   ├── index.php
│   └── Dockerfile
```

---

## 📝 1. Crée un fichier `index.php`

Dans le dossier `site/` :

```php
<?php
$pdo = new PDO("mysql:host=db;dbname=test", "root", "root");
echo "<h1>Connexion MySQL réussie !</h1>";

```

---

## 📝 2. Crée un `Dockerfile` dans `site/`

```Dockerfile
FROM php:8.0-apache
WORKDIR /var/www/html
COPY . .
EXPOSE 80
```

---

## ⚙️ 3. Crée le fichier `docker-compose.yml`

À la racine du projet :

```yaml
version: "3.8"

services:
  web:
    build: ./site
    ports:
      - "8080:80"
    depends_on:
      - db

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: test
    volumes:
      - db_data:/var/lib/mysql

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    restart: always
    ports:
      - "8081:80"
    environment:
      PMA_HOST: db
      MYSQL_ROOT_PASSWORD: root
    depends_on:
      - db

volumes:
  db_data:
```

---

## 🚀 4. Lancer les conteneurs

Dans le terminal, à la racine du projet :

```bash
docker-compose up --build -d
```

---

## 🔍 5. Vérifier

- Site web : [http://localhost:8080](http://localhost:8080)
- Interface phpMyAdmin : [http://localhost:8081](http://localhost:8081)

---

## 🧼 6. Nettoyage

Arrêter et supprimer tous les services :

```bash
docker-compose down -v
```

## ✅ Critères de réussite

- Les trois conteneurs fonctionnent
- Le site PHP se connecte bien à la base MySQL
- L’interface phpMyAdmin est accessible

---

> Tu viens de créer un environnement web complet avec Docker Compose ! Bravo 🎉
