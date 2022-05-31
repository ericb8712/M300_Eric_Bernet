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




## Quellen
https://tbzedu.sharepoint.com/sites/campus/students/it/Forms/AllItems.aspx?id=%2Fsites%2Fcampus%2Fstudents%2Fit%2F%5Fread%2Donly%2FM300%2F2%2D%20Unterlagen%2FDocker%5Fcheat%2Dsheet%2Dv2%2Epdf&parent=%2Fsites%2Fcampus%2Fstudents%2Fit%2F%5Fread%2Donly%2FM300%2F2%2D%20Unterlagen&p=true&ga=1