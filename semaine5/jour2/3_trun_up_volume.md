**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5 - Containers et orchestration**

**Jour 2 : Compose**

---

# 3 - Turn up the volume

## 1 - SANS VOLUME

👉 Reprenez le fichier Docker Compose du challenge précédent "Web compose" et démarrez le service "nginx".

N'oubliez pas de mettre les fichier de nginx.conf et index.html modifiés dans le dossier projet host

👉 Trouver un moyen d’exécuter l'interpréteur de commande bash dans le conteneur lié au service "nginx" via la commande docker-compose.

```
docker compose exec -it <NOM DU SERVICE DANS LE YAML> /bin/bash
```
> [!WARNING]
> Différent de docker exec -it \<ID ou NAME du CONTAINER\>

> [!TIP]
> En cas de problème, n'hésitez pas à RESET ALL :
```
docker compose down
(si permission denied: sudo aa-remove-unknown)
docker container rm <ID CONTAINERS>
docker image rm <ID IMAGE>
docker system prune [--all]
sudo systemctl restart docker
```

👉 Une fois le terminal du conteneur disponible et attaché, exécutez la commande suivante afin de remplacer rapidement le contenu du fichier HTML utilisé par défaut par le serveur web.

```
echo "<p>This is a test</p>" > /usr/share/nginx/html/index-lacapsule.html
```

👉 Quittez le terminal interactif du conteneur et faites une requête vers le serveur web via curl afin de constater la modification.

👉 Arrêtez et supprimez le conteneur lié au service "nginx".

👉 Démarrez de nouveau le service nginx afin de refaire une requête vers le serveur web via curl.

Vous constatez que le fichier HTML originel est revenu, car ce qui se passe dans le conteneur est temporaire, il n’y a que ce qui est enregistré dans l’image qui sera conservé en cas de suppression du conteneur (du moins, pour le moment)

## 2 - AVEC VOLUME

👉 Grâce à la documentation et la notion de volumes Docker, trouvez les instructions à ajouter dans le fichier Docker Compose afin que le dossier "/usr/share/nginx/html" soit monté (bind mount) sur la machine hôte.
_Ce dossier devra s’appeler "html" et sera automatiquement créé dans le même dossier que le fichier "docker-compose.yml" sur la machine hôte._

```
services:
  nginx:
    build: .
    ports:
      - 8080:81
    volumes:
      - ./html:/usr/share/nginx/html
```

👉 Démarrez le service "nginx" et vérifiez que le dossier "html" a bien été créé sur la machine hôte.

👉 À l’intérieur de ce dossier "html", créez un fichier "index-lacapsule.html" avec le contenu de votre choix et redédmarrrez les services. Exécutez un curl pour vérifier que les modifs du index.html sont ok

```
curl http://localhost:8080
```

_Si le dossier a été créé automatiquement par Docker, il a très certainement les permissions root, il faudra donc modifier ses permissions **POUR L'ATTIBUER AU USER QUI RUN DOCKER COMPOSE**._
