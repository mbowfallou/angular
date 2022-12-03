# MyApp

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 15.0.0.

# ReadMe File -- Angular

Pour executer cette application sur votre machine, vous devez d'abord avoir
- Docker(engine) installé
- Une connexion si vous n'avez pas les images de node et nginx

## Ce qui va se passer dans ce Dockerfile 

```

Pour la partie NODE

```

###### Création à partir de l'Image de NODE
* FROM node:latest AS builder
###### Définition de l'espace de travail de Node
* WORKDIR /app
###### Copie du contenu courant vers l'espace de travail
* COPY . .
###### Installation des packages et construction de l'application
* RUN npm install && npm run build

```

Pour la partie NGINX

```

###### Création à partir de l'Image de NGINX
* FROM nginx:alpine
###### Définition de l'espace de travail de Nginx
* WORKDIR /usr/share/nginx/html
###### Suppression des fichiers statics par defaut de Nginx
* RUN rm -rf ./*
###### Copie du contenu de "builder" vers l'espace de travail de Nginx
* COPY --from=builder /app/dist/my-app .
###### Exécution de Nginx globallement et Arret de daemon
* ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

C'est terminé, et : 
Pour executer ce fichier pour Docker: docker build <root-app> -t tag_name
Création du conteneur : docker run --rm --name my-app -p 8080:80 my-app-image

```sh
npm install --production
NODE_ENV=production node app
```

