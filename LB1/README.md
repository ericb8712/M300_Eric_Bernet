# Einleitung
Einleitung zum LB1 Projekt (Erklärungen)

# Inhaltsverszeichnis

## Service-Aufbau 

auf dem server file erstellen mit diesem namen:
docker-compose.yaml

das file sollte diesen inhalt haben: Quelle:
[Text](https://hub.docker.com/_/nextcloud)

###############
version: '2'

volumes:
  nextcloud:
  db:

services:
  db:
    image: mariadb
    restart: always
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    volumes:
      - db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=
      - MYSQL_PASSWORD=
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud

  app:
    image: nextcloud
    restart: always
    links:
      - db
    volumes:
      - nextcloud:/var/www/html
    environment:
      - MYSQL_PASSWORD=
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db
###############





## Umsetzung
Text

## Testing
Text

## Quellen
[Text](https://hub.docker.com/_/nextcloud)

