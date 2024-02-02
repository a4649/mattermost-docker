# mattermost-docker
Mattermost deployment using docker

# How To

Copy environment template

```
cp env.example .env
```

Adjust env vars

Create folders:

```
mkdir -p /srv/mattermost/{config,data,logs,plugins,client/plugins,bleve-indexes}
sudo chown -R 2000:2000 /srv/mattermost
```

Deploy:

```
docker compose -f docker-compose.yml up -d
```

Navigate to http://<docker-host>:8065/ in your browser

# Backup

Database:

```
docker exec -t postgres pg_dumpall -c -U postgres | gzip > ./mattermost-db_$(date +"%Y-%m-%d_%H_%M_%S").gz
```

Mattermost config file:

```
cp  /srv/mattermost/config/config.json  /opt/backups/config.json_$(date +"%Y-%m-%d_%H_%M_%S")
```

Files stored by users:

```
cp -rav /srv/mattermost/data /opt/backups/data_$(date +"%Y-%m-%d_%H_%M_%S")
```

Based on [Mattermost Docker](https://github.com/mattermost/docker)