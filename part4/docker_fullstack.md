# 🐳 TP Docker avancé — Projet PHP MVC avec Composer & PHPUnit

Dans ce TP, tu vas dockeriser un **vrai projet PHP en architecture MVC**, incluant Composer, PHPUnit et un environnement complet via Docker Compose.

---

## 🎯 Objectif

- Cloner un projet MVC PHP existant
- Créer un `Dockerfile` adapté avec Composer & Apache
- Ajouter les dépendances via Composer
- Exécuter les tests unitaires avec PHPUnit
- Configurer un environnement complet avec Docker Compose (PHP, Apache, MySQL, phpMyAdmin)

---

## 🔗 Étapes

### 1. Cloner le dépôt

```bash
git clone https://gitlab.com/dev3632212/projectdocker#
cd <nom_du_projet>
```

---

### 2. Structure recommandée du projet

```
mon-projet/
├── app/
├── public/
│   └── index.php
├── tests/
├── composer.json
├── Dockerfile
├── docker-compose.yml
└── .dockerignore
```

### 4. Crée ton `Dockerfile`

```Dockerfile
FROM php:8.0-apache

# Installe les extensions nécessaires
RUN

# Installe Composer

# Définit le répertoire de travail
WORKDIR /var/www/html

# Copie le code source
COPY . .

EXPOSE 80
```

---

### 5. Crée ton `docker-compose.yml` exemple

```yaml
version: "3.8"

services:
  web:
    build: .
    ports:
      - "8080:80"
    volumes:
      - .:/var/www/html
    depends_on:
      - db

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: mvc
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

volumes:
  db_data:
```

---

### 6. Lancer le projet

```bash
docker-compose up --build -d
```

Accède à ton site sur : [http://localhost:8080](http://localhost:8080)  
Et à phpMyAdmin : [http://localhost:8081](http://localhost:8081)

---

### 7. Exécuter les tests unitaires (PHPUnit)

Dans le conteneur PHP :

```bash
docker-compose exec web vendor/bin/phpunit
```

---

## 📤 Livrables attendus

- `Dockerfile` fonctionnel avec Composer
- `docker-compose.yml`
- Capture de la page d'accueil du projet MVC
- Capture de l'exécution des tests PHPUnit

---

## ✅ Critères de performance

- L’environnement se lance sans erreur
- Les dépendances sont gérées avec Composer
- Les tests PHPUnit sont exécutés avec succès
- L’architecture MVC est préservée

---

> Tu viens de dockeriser un projet PHP complet avec gestion des dépendances et des tests 🎉
