
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

## 02 - Verwendetet Tools

## 03 - Wissenstand

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
! Container: redis-master Database - no public IP               !
! Container: redis-slave Database - no public IP                !
+---------------------------------------------------------------+
! Container-Engine: Docker                                      !
+---------------------------------------------------------------+
! Kubernetes Umgebung Google Cloud (GKE) - 3 Node Cluster       !
+---------------------------------------------------------------+
! Notebook HP EliteBook - Schulnetz 10.x.x.x                    !
+---------------------------------------------------------------+

### 04.4 - Image
Für dieses Projekt habe ich die Redis Image vom Dockerhub verwendet. Kubernetes bezieht diese dann automatisch von dort.

### 04.5 - Memory
Das es sich um Memory-Datenbanken handelt habe ich diesen 7.5 GB Memory in der Google Cloud zurverfügung gestellt. 

## 05 - Sicherheitsaspekte

### 05.1 - Logs
In der Kubernetes-Umgebung kann man logs mit dem folgendem Befehl abrufen: kubectl logs <pod-name>
  
### 05.2 - Monitoring
Alles Kann auf der Google Cloud Plattform über die Web-Konsole Überwacht werden wie zum Beispiel CPU, Speicher oder Laufwerk.

### 05.3 - Containersicherheit
- PHP Guestbook Frontend ist unter dem Port 80 anzufinden dies konnte mit dem Loadbalance so eingerichtet werden
- Redis Master und der Redis Slave sind nur Intern erreichbar um änderungen an den Datensätze von Angriffen zu verhindern
- Container laufen in einer dedizierten virtuellen Maschine in der Google Cloud
- Der Redis Slave unterstützt den Redis Master automatisch bei hohem Traffic  

## 07 - Testfälle

## 08 - Wissenszuwachs

## 09 - Reflektion

