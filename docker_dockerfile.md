# 🐳 Docker - Anatomie d'un Dockerfile (Customisation de php:8.0-apache)

Apprends à **créer et personnaliser une image Docker** en te basant sur une image officielle existante.

---

## 🎯 Objectif pédagogique

- Comprendre la structure d’un `Dockerfile`
- Personnaliser une image Docker existante (`php:8.0-apache`)
- Ajouter son propre code dans l’image
- Lancer et tester le conteneur localement

---

## 📚 Ressources utiles

- [Best practices Dockerfile](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Référence Dockerfile](https://docs.docker.com/reference/dockerfile/)
- [.dockerignore guide](https://shisho.dev/blog/posts/how-to-use-dockerignore/)
- [Exemple .dockerignore](https://github.com/BretFisher/node-docker-good-defaults/blob/main/.dockerignore)

---

## 🔧 Contexte du TP

Tu souhaites créer un site web simple en PHP. Pour cela, tu vas personnaliser l’image officielle `php:8.0-apache`.

L’idée : ajouter **ton propre code HTML/PHP** dans l’image, grâce à un `Dockerfile` minimaliste.

---

## 📁 Prépare ton projet

1. Crée un dossier `site-personnel`
2. À l’intérieur, crée un fichier `index.php` :

```php
<?php echo "<h1>Bienvenue dans mon site customisé avec Docker !</h1>"; ?>
```

3. Crée un fichier `.dockerignore` :

```
.git
node_modules
*.log
Dockerfile
```

---

## 📝 Crée le Dockerfile

Toujours dans `site-personnel`, crée un fichier `Dockerfile` :

```Dockerfile
FROM php:8.0-apache
WORKDIR /var/www/html
COPY . .
EXPOSE 80
```

---

## 🏗️ Construis l’image

Dans le terminal, place-toi dans le dossier `site-personnel` :

```bash
docker build -t mon-site-custom .
```

---

## 🚀 Lance le conteneur

```bash
docker run -d -p 8080:80 mon-site-custom
```

➡️ Ouvre ton navigateur : http://localhost:8080

Tu dois voir ton message personnalisé en PHP.

---

## 🔍 Vérifie

- Liste les images : `docker images`
- Liste les conteneurs : `docker ps`
- Voir les logs (en cas d’erreur) : `docker logs <id_du_conteneur>`

---

## 🧼 Nettoyage (optionnel)

```bash
docker stop <id>
docker rm <id>
docker rmi mon-site-custom
```

---

## 🧾 Livrables attendus

- Contenu du `Dockerfile`
- Capture d’écran du navigateur sur `http://localhost:8080`

---

## ✅ Critères de réussite

- L’image est correctement construite
- Le conteneur fonctionne et sert le fichier PHP
- Le Dockerfile est propre et compréhensible

---

> Bravo ! Tu sais maintenant comment créer une image Docker personnalisée en te basant sur une image officielle. 🎉

---

## ☁️ Pousser l’image sur Docker Hub (facultatif mais recommandé)

Si tu as un compte Docker Hub, tu peux publier ton image pour la partager ou la réutiliser plus facilement.

### 🧩 Étapes à suivre

1. Connecte-toi à Docker depuis ton terminal :

```bash
docker login
```

> Entrez votre identifiant et mot de passe Docker Hub.

2. Renomme ton image avec ton identifiant Docker :

```bash
docker tag mon-site-custom ton_identifiant_docker/mon-site-custom
```

> Exemple : `docker tag mon-site-custom johndoe/mon-site-custom`

3. Envoie ton image sur Docker Hub :

```bash
docker push ton_identifiant_docker/mon-site-custom
```

4. Vérifie sur [hub.docker.com](https://hub.docker.com/) que ton image est bien listée dans ton compte.

---

## 📤 Bonus à livrer (optionnel)

- Le lien public vers ton image Docker sur Docker Hub (ex: https://hub.docker.com/r/ton_identifiant/mon-site-custom)

---

> Tu maîtrises désormais la chaîne complète : création, exécution et publication d’une image Docker personnalisée ! 🐳🚀
