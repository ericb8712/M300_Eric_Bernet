# Einleitung
Einleitung zum LB1 Projekt (Erklärungen)

# Inhaltsverszeichnis

## Service-Aufbau 


(für dieses Projekt muss man Nginx und docker installieren)
<br>
auf dem server file erstellen mit diesem namen:
docker-compose.yaml
<br>
das file sollte diesen inhalt haben: Quelle:
[Text](https://hub.docker.com/_/nextcloud)
<br>
Dazu sollte man dem Webserver noch eine statische IP Adresse geben, sodass sie immer die gleiche hat. 
Dazu sollte man die vorlage mit den beiden code schnipsel networks, anpassen.
<br>
```yaml
version: '2'

networks:
  mynetwork:
    ipam:
      config:
        - subnet: 172.20.0.0/24

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
      - MYSQL_ROOT_PASSWORD=eric123
      - MYSQL_PASSWORD=eric123
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
      - MYSQL_PASSWORD=eric123
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db
    ports:
      - "8080"
    networks:
      default:
      mynetwork:
        ipv4_address: 172.20.0.6
```
<br>
nach dem man das dockercompose file erstellt und gespeichert hat muss man den befehl unten aufgeführt ausführen und das ganze zu starten:
<br>
docker-compose up -d
<br>



im ngnix im file /etc/nginx/sites-enabled/default das default file anpassen mit:
<br>

```yaml
server {
        listen 80;
        listen [::]:80;
        server_name sharoneric.com;
    root /var/www/sharoneric.com;
        location / {
        proxy_pass http://172.20.0.6:80/;
    proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header   Host $http_host;
        proxy_set_header   X-Forwarded-Proto $scheme;
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;

        proxy_connect_timeout 30;
        proxy_send_timeout 30;
        proxy_read_timeout 30;

        }
}
```



<br>

zum schluss noch im unten aufgeführten file einen eintrag anpassen
<br>
%windir%\system32\drivers\etc\hosts
<br>
anpassen mit: sharoneric.com
<br>

## Umsetzung
Text

## Testing
Text

## Quellen
[Text](https://hub.docker.com/_/nextcloud)

