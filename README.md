# abes-filebeat-docker

Contient la configuration du filebeat déployé sur un nœud docker à l'Abes qui permet d'envoyer les logs des conteneurs vers le puits de logs de l'Abes.

## Installation

```
cd /opt/pod
git clone https://github.com/abes-esr/abes-filebeat-docker.git
cd abes-filebeat-docker

cp .env-dist .env
# personnaliser ensuite les variables souhaitées dans le .env
# en particulier LOGSTASH_HOST
```

## Démarrage et arret

```bash
# pour démarrer
cd /opt/pod/abes-filebeat-docker/
docker-compose up -d

# pour stopper
cd /opt/pod/abes-filebeat-docker/
docker-compose stop

# pour voir les logs
cd /opt/pod/abes-filebeat-docker/
docker-compose logs -f --tail=50
```
## Debug

Une [application exemple est disponible dans ce depot](https://github.com/abes-esr/abes-filebeat-docker/blob/d04c5d1c5f641dd35ee632a2a61a7215b0a432aa/docker-compose.yml#L24-L38) qui pourra envoyer des logs au format nginx.
Pour la lancer et pour générer une ligne de log avec curl :
```bash
cd /opt/pod/abes-filebeat-docker/
docker-compose --profile=debug up -d
curl http://127.0.0.1:8081
```

Pour la stopper :
```bash
cd /opt/pod/abes-filebeat-docker/
docker-compose stop abes-filebeat-app-exemple
```

Il est également possible d'ajouter des traces au niveau de filebeat lui même pour par exemple voir les messages JSON avant que filebeat ne les envoi à logstash, pour cela modifier [la ligne suivante](https://github.com/abes-esr/abes-filebeat-docker/blob/f4b19dfdccab690801c550c61724bd09cbeb6f5b/docker-compose.yml#L20) comme ceci et relancer le conteneur abes-filebeat-docker :
```yml
    command: ["-e", "--strict.perms=false", "--d=*"]
```
ou comme ceci pour n'avoir que le debug des logs envoyées à logstash :
```yml
    command: ["-e", "--strict.perms=false", "--d=processors"]
```
