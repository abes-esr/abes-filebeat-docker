# abes-filebeat-docker

Contient la configuration du filebeat déployé sur un nœud docker à l'Abes qui permet d'envoyer les logs des conteneurs vers le puits de logs de l'Abes (travail en cours)

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

```
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

Une application exemple est disponible dans ce depot qui pourra envoyer des logs au format nginx.
Pour la lancer et pour générer une ligne de log avec curl :
```
docker-compose --profile=debug up -d
curl http://127.0.0.1:8081
```

