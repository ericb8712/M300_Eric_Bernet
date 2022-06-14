# Docker

Als erstes habe ich die seite hub.docker.com aufgerfen. Auf dieser seite sind alle Images hinterlegt, ein Image ist eine Datei, die aus mehreren Schichten besteht und zur Ausführung von Code in einem Docker-Container verwendet wird. Ein Image wird im Wesentlichen aus den Anweisungen für eine vollständige und ausführbare Version einer Anwendung erstellt, die sich auf den Kernel des Host-Betriebssystems stützt. Wenn der Docker-Benutzer ein Image ausführt, kann es zu einer oder mehreren Instanzen dieses Containers werden.


# Wichtige Commands:

docker pull ubuntu/mysql
docker images
docker run -d --name mysqlcontainerEricModul300 -e TZ=UTC -p 3306:3306 -e MYSQL_ROOT_PASSWORD=mysql ubuntu/mysql:8.0-22.04_beta
docker exec -it ddaf2c531646 /bin/bash
docker ps
docker start ddaf2c531646

# Vorgehen
Als erstes lade ich das Image herunter mit dem Command:

docker pull ubuntu/mysql

Dieser Schritt ist eigentlich nicht notwendig, denn später wird ein Image, das noch nicht lokal vorhanden ist, aber ausgeführt werden soll, automatisch heruntergeladen. Nach dem Namen des Abbilds kann man die Version des Abbilds angeben, getrennt durch ein ":"; wenn man nichts angibt, wird automatisch die neueste Version heruntergeladen.

Mit dem folgenden Befehl kann man herausfinde, welche Images lokal schon vorhanden sind.

docker images

Mit dem folgenden Befehl wird das Image in einem Container gestartet. Falls das Image hier noch nict heruntergeladen ist wird es jetzt automatisch gepullt. Der Run Befehl besteht aus folgenden Teilen:

docker run -d --name mysqlcontainerEricModul300 -e TZ=UTC -p 3306:3306 -e MYSQL_ROOT_PASSWORD=mysql ubuntu/mysql:8.0-22.04_beta

docker run um zu sagen was man überhaupt will container stoppen oder starten
-d detach um wieder zurück auf die Commandozeile zu kommen
-- name um den Namen des Containers anzugeben
-e TZ= um die Timezone des Servers zu setzten
-e MYSQL_ROOT_PASSWORD= um das Root Passwort des Sql Servers zu definieren
-p um das Port forwarding einzurichten also anfragen welche der Host auf "3306" bekommt werden intern auf den Port "3306" weitergeleitet, auf welchem der Docker Deamon wartet. wie bei einer VM und hinten noch das image mit ":" um die Version anzugeben
Mit: docker exec -it mysql-container /bin/bash

kann man auf den Container selber verbinden, wie wenn man auf eine VM verbindet, wenn man connectet ist, kann man unter /var/lib/mysql seine Tables sehen

Um den Container zu stoppen, "herunterzufahren": 

docker stop idvomContainer


# Volume
docker run -d --name eric-mysql-container -e TZ=UTC -v modul300:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=mysql ubuntu/mysql:8.0-22.04_beta

-v beschreibt wo das volume speichern sollte. in diesem Beispiel heisst das Volume modul300 (ist auf der vm gespeichert)und wird dann im /var/lib/mysql im container abgelegt, sodass es die daten nicht verliert wenn man den container löscht. Das heisst man kann den container löschen ohni die daten zu verlieren.


# Images
image ab einem laufenden container bilden:

docker run -it --name variante1 --hostname variante1 ubuntu bash
docker exec -it variante1 bash

laufender conainter(variante1 in diesem fall) zu einem Image machen:
docker commit variante1 img/variante1

# Docker files
Docker file erstellen:
docker build -t df/variante2 .

container mit docker file starten:
docker run --rm -d --name variante2 -p 80:80 df/variante2

# Netzwerk
Netzwerk erstellen:
docker network create mynetwork

alle container, welche in diesem Netzwerk sind können miteinander kommunizieren. 

mit dem folgenden befehl kann man alle netzwerke löschen, welche nicht gebracuht werden. 
docker network prune




Docker image Docker HUB

Wichtig: Man braucht ein Docker hub account

Gitlab von Herr Calisto copieren:

"TEMP_Docker" erstellen:
$ mkdir TEMP_Docker Unterverzeichnis 

Ins Unterverzeichnis "TEMP_Docker" wechseln
$ cd TEMP_Docker 

Repo klonen
$ git clone https://gitlab.com/ser-cal/Container-CAL-webapp_v1.git 

ins Repo-Unterverzeichnis wechseln
$ cd Container-CAL-webapp-v1/ 

Ins Unte
$ cd APP 

das File views/home.pug ist da um die Homepage zu bearbeiten

nach dem ein Image erstellen, name durch namen ersetzten.
$ docker image build -t <name>/webapp_one:1.0 .

jetzt sich mit seinem dockker Account einlogen:
$ docker login --username=<name>

Danach das image auf docker hub pushen:
$ docker image push <name>do/webapp_one:1.0

Jetzt nur noch die den Container starten:
$ docker container run -d --name eric-web -p 8080:8080 ericbernet/webapp_one:1.0

container stopen
$ docker container stop 8c6

container löschen
$ docker container rm 8c6


2 container erstellen 
$ docker container run -d --name eric-web2 -p 8080:8080 ericbernet/webapp_two:2.0

image auf docker hub pushen
$ docker image push ericbernet/webapp_two:2.0

<img src="bild1">




## Quellen
https://tbzedu.sharepoint.com/sites/campus/students/it/Forms/AllItems.aspx?id=%2Fsites%2Fcampus%2Fstudents%2Fit%2F%5Fread%2Donly%2FM300%2F2%2D%20Unterlagen%2FDocker%5Fcheat%2Dsheet%2Dv2%2Epdf&parent=%2Fsites%2Fcampus%2Fstudents%2Fit%2F%5Fread%2Donly%2FM300%2F2%2D%20Unterlagen&p=true&ga=1