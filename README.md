# Cours de Devops 2023

## 1-1 Document your database container essentials: commands and Dockerfile.

Voici ma commande qui permet de lancer la database:

```bash
docker run -p 8888:80 --network app-network -v /data:/var/lib/postgresql/data --name tp tp/vincent
```

l'option `-p` permet d'exposer un port.

l'option `--network` permet d'associer un network existant.

l'option `-v` permet de créer un volume entre la machine locale et le container docker.

l'option `--name` permet de donner un nom au container.

Voici mon Dockerfile:

```
FROM postgres:14.1-alpine

ENV POSTGRES_DB=db \
	POSTGRES_USER=usr \
	POSTGRES_PASSWORD=pwd

COPY ./scripts/ /docker-entrypoint-initdb.d 
```

Le `FROM` permet de récupérer une image sur un dépot par exemple DockerHub.

Le `ENV` permet d'écrire des variables d'environnements.

Le `COPY` permet de copier un fichier ou un répertoire vers le container Docker.

## 1-2 Why do we need a multistage build? And explain each step of this dockerfile.

Le build à plusieurs étape permet de séparer les étapes de constructions de l'image, mais aussi cela permet de mieux comprendre le DockerFile et reste maintenable par tout le monde.

La première étape commence par définir une image de base à partir de laquelle construire.

Le `ENV` permet d'écrire des variables d'environnements.

Le `WORKDIR` permet de changer le répertoir actuel avec celui spécifié.

Les `COPY`, cf question précédentes.

Le `RUN` exécute une commande maven sans faire les tests lors du build.

Pour la seconde partie, on commence par spécifier une autre image.

Les commandes `ENV, WORKDIR, COPY` cf questions précedentes.

Le `ENTRYPOINT` déinit la commande d'exécution lorsque le conteneur démarre.

## 1-3 Document docker-compose most important commands.

Il suffit de faire un `docker-compose un --build` 

L'option `--build` dans la commande `docker-compose up --build` permet de reconstruire les images Docker des services spécifiés dans le fichier docker-compose.yml avant de les démarrer.

## 1-4 Document your docker-compose file.

Voir les commentaires dans le docker-compose.yml

## 1-5 Document your publication commands and published images in dockerhub.

Voici les commandes qui permettent de mettre un tag sur les 3 images avant de les publier.

```
docker tag dv-backend shinichiv2/backend:1.0
docker tag dv-httpd shinichiv2/httpd:1.0
docker tag dv-database shinichiv2/database:1.0
```

Et voici les commandes qui permettent de publier l'image sur le compte dockerHub spécifier:

```
docker push shinichiv2/backend:1.0
docker push shinichiv2/httpd:1.0
docker push shinichiv2/database:1.0
```

## 2-1 What are testcontainers?

Testcontainers est une bibliothèque Java qui permet de créer et de gérer facilement des conteneurs légers et éphémères pour les tests d'intégration. Il utilise Docker pour créer des environnements de test conteneurisés.

## 2-2 Document your Github Actions configurations.

Voir les fichiers de configurations qui se trouvent dans le dossier `.github/workflows`

## Document your quality gate configuration.

Voir le fichier `.github/workflows/test_backend.yml` à la ligne 27.


