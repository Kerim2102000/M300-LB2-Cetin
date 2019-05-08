
# **Modul 300 LB2 Dokumentation** 

# Inhaltsverzeichnis
  - [01 - Umgebung](#01---umgebung)
  - [02 - Verwendetet Tools](#02---verwendetet-tools)
  - [03 - Wissenstand](#03---wissenstand)
  - [04 - Sicherheitsaspekte](#04---Sicherheitsaspekte)
  - [05 - Testfälle](#05---Testfälle)
  - [06 - Wissenszuwachs](#06---Wissenszuwachs)
  - [07 - Reflektion](#07---Reflektion)

## 01 - Umgebung

- Google Cloud Plattform
- Docker Desktop
- Visual Studio Code

## 02 - Verwendetet Tools

- Google Cloud Plattform
- Docker Desktop
- Dockerhub
- Visual Studio Code
- Git-Client (inkl. SSH-Key)

## 03 - Wissenstand

### 03.1 - Linux
Linux Grundkenntnisse sind vorhanden jedoch im Betrieb eher gelegentlich zu tun. Zu hause ein paar Test VMs gemacht um in das Thema besser reinzukommen und Erfahrungen zu sammeln.

### 03.2 - Virtualisierung
Erfahrung in Virtualisierung mit ESXi, VMware und Virtual Box. Server Umgebungen Virtualisierung im Betrieb geplant und ausgeführt.

### 03.3 - Vagrant
Vorkenntnisse von der LB2 vorhanden

### 03.4 - Versionverwaltung
Erfahrung im Betrieb mit Versionverwaltung Document Management Systemen und Cloud. Mit GitHub noch wenige Erfahrungen gemacht. Grundsätzlich sollte es mir nicht schwer fallen mit GitHub zu arbeiten.

### 03.5 - Markdown
Noch keine Vorkenntnisse vorhanden.

### 03.6 - Systemsicherheit
Firewalls im Betrieb konfiguriert Linux Basierend SonicWall, ZyWALL, Cisco. Planung von Sicherheitskonzepten schon in der TBZ realsiert.

### 03.7 - Containersierung
Bisher keine Erfahrung mit Containerisierung gesammelt, noch nie damit gearbeitet.

### 03.8 - Docker
Keine Vorkenntnisse mit Docker vorhanden, noch nie damit gearbeitet.

### 03.9 - Micros Service
Noch keine Vorkenntnisse vorhanden.

### 03.1 - Docker Befehle

| Befehl       | Beschreibung                                       |
| ------------ | -------------------------------------------------- |
| docker run   | Führt ein Befehl in einem neuen Container aus      |
| docker start | Startet einen oder mehrere gestoppte Container     |
| docker stop  | Stoppt einen oder mehrere laufende ontainer        |
| docker build | Erstellt ein Image aus einem Docker-File           |
| docker pull  | Ladet ein Image aus der Registry                   |
| docker push  | Ladet ein Image in die Registry hoch               |
| docker exec  | Führ einen Befehl in einem laufenden Container aus |

## 04 - Umsetzung

### 04.1 - Projektbezeichnung
Es handelt sich um eine mehrschichtige Webanwendung die mit Hilfe von der Google Cloud erstellt wurde. Die Applikation ist ein Gästebuchrd, in dem Besucher Text in ein Log eingeben und die letzten geloggten Einträge sehen können. Diese Einträge werden in einer Redis Datenbank erfasst diese hat den Vorteil weil sie eine Memory-Datenbank verwedendet sie den Arbeitsspeicher und erlaubt so höhere Zugriffsgeschwindigkeiten.

### 04.3 - Netzwerkplan

    +---------------------------------------------------------------+
    ! Container: Guestbook Frontend PHP - 104.154.89.159:80         !
    ! Container: Redis-Master Database  - no public IP              !
    ! Container: Redis-Slave Database - no public IP                !
    +---------------------------------------------------------------+
    ! Container-Engine: Docker                                      !
    +---------------------------------------------------------------+
    ! Kubernetes Umgebung Google Cloud (GKE) - 3 Node Cluster       !
    +---------------------------------------------------------------+
    ! Notebook HP Elitebook Windows 10 - Schulnetz 10.x.x.x         !
    +---------------------------------------------------------------+


### 04.4 - Image
Für dieses Projekt habe ich die Offiziellen Redis Image vom Dockerhub verwendet. Kubernetes bezieht diese dann automatisch von dort.

### 04.5 - Memory
Das es sich um Memory-Datenbanken handelt habe ich diesen 7.5 GB Memory in der Google Cloud zurverfügung gestellt. 

## 05 - Sicherheitsaspekte

### 05.1 - Logs
In der Kubernetes-Umgebung kann man logs mit dem folgendem Befehl abrufen: kubectl logs <pod-name>
  
### 05.2 - Monitoring
Alles Kann auf der Google Cloud Plattform über die Web-Konsole Überwacht werden wie zum Beispiel CPU, Speicher oder Laufwerk auslastung.

### 05.3 - Containersicherheit
- PHP Guestbook Frontend ist unter dem Port 80 anzufinden dies konnte mit dem Loadbalance so eingerichtet werden
- Redis Master und der Redis Slave sind nur Intern erreichbar um änderungen an den Datensätze von Angriffen zu verhindern
- Container laufen in einer dedizierten virtuellen Maschine in der Google Cloud
- Der Redis Slave unterstützt den Redis Master automatisch bei hohem Traffic  

## 07 - Testfälle

|   Test| Resultat  |
|---|:-:|
| Vom Client auf http://104.154.89.159:80 zugreifen  | Funktioniert. Das Guestbook (104.154.89.159:80 ) wird angezeigt  |
| Vom Client auf den Webserver (192.168.10.101) zugreifen per SSH |  Funktioniert, da eine SSH Verbindung vom Client her zugelassen wurde in der Firewall |
| Vom Client auf die Datenbank (192.168.10.100) zugreifen per SSH |  Funktioniert, da eine SSH Verbindung vom Client her zugelassen wurde in der Firewall |
| Mit dem Admin User sich auf die Datenbank anmelden | Die Datenbank aktzeptiert den zugang des Webserver mit dem Admin User|
       
## 08 - Wissenszuwachs

Ich habe viele neue Sachen gelernt im Bezug von Docker und Kubernetes mit der Google Cloud Plattform und dessen Aufbau und das zusammen spiel eines Docker Images.   

## 09 - Reflektion
Die LB02 verlief im Grunde genommen ganzen gut. Das Realisieren von Kubernets Container in der Google Cloud war sehr interessant und lehrreich. Am Anfang musste ich mich mit Docker ein wenig zurecht finde genauer gesagt das Erstellen eines Images. Doch dies konnte ich mit Hilfe von Foren ausgleichen. Mit dieser LB2 habe ich Docker und Kubernetes viel besser kennen gelernt. Die enorme Vielfalt von Google Cloud hat mich sehr überrascht und fasziniert dort mit Kubernetes Container zu erstellen. Zeitlich bin ich gut mit der LB2 durchgekommen und bin mit meiner Arbeit zufrieden. 

