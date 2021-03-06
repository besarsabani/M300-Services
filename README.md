# M300-Services
So bin ich für die LB2 vorgegangen.

## Inhaltsverzeichnis
- [M300-Services](#m300-services)
  - [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [K1](#k1)
  - [Virtualbox](#virtualbox)
    - [Software herunterladen & installieren](#software-herunterladen--installieren)
    - [ISO-Datei herunterladen](#iso-datei-herunterladen)
    - [VM erstellen](#vm-erstellen)
    - [VM einrichten](#vm-einrichten)
  - [Vagrant](#vagrant)
    - [Vm erstellen mit abgeändertem File](#vm-erstellen-mit-abge%C3%A4ndertem-file)
  - [Visualstudio-Code](#visualstudio-code)
  - [Git-Client](#git-client)
  - [ssh-Key](#ssh-key)
- [K2](#k2)
  - [GitHub Account](#github-account)
- [K3](#k3)
  - [Testen](#testen)
    - [Apache](#apache)
    - [Users-and-Groups](#users-and-groups)
    - [Ports](#ports)
- [K4](#k4)
  - [Firewall](#firewall)
  - [Benutzer-und-Rechtevergabe](#benutzer-und-rechtevergabe)
  - [SSH](#ssh)
- [K5](#k5)
  - [Vergleich Vorwissen - Wissenszuwachs](#vergleich-vorwissen---wissenszuwachs)
  - [Reflexion](#reflexion)
- [LB3-Docker](#lb3-docker)
  - [K1-LB3](#k1-lb3)
  - [K2-LB3](#k2-lb3)
  - [Vorwissen zu Docker](#vorwissen-zu-docker)
  - [K3-Docker](#k3-docker)
    - [Docker Container](#docker-container)
    - [Backend-Frontend](#backend-frontend)
    - [Volumes für Datenablage](#volumes-f%C3%BCr-datenablage)
    - [Docker Spezifische Befehle](#docker-spezifische-befehle)
  - [Funktion](#funktion)
  - [Sicherheit](#sicherheit)
    - [Image Poisoning](#image-poisoning)
    - [Ressourcen Limiten angeben](#ressourcen-limiten-angeben)
    - [Benachrichtungen](#benachrichtungen)

K1
===
> [⇧ *Nach oben*](#inhaltsverzeichnis)

## Virtualbox

### Software herunterladen & installieren
   Zuerst habe ich die Software heruntergeladen und installiert. dies habe ich auf der Webseite "www.virtualbox.org" gemacht. Als ich alles Installiert habe, habe ich ich eine ISO-datei heruntergeladen.


### ISO-Datei herunterladen
Zuerst habe Ich hierfür ein Ubuntu Image heruntergeladen. Diese ISO Datei habe ich auf der Webseite "www.ubuntu.com" gefunden. Nun kann es losgehen, man kann ubuntu Vm's erstellen.

### VM erstellen
Nun erstellt man die VM. man geht folgendermassen vor.
1. VirtualBox starten
2. Links oben, innerhalb der Anwendung, auf `Neu` klicken
3. Im neuen Fenster folgende Informationen eintragen:
   *  Name:           `M300_Ubuntu_XX.04_Desktop`
   *  Typ:            `Linux`
   *  Version:        `Ubuntu (64-bit)`
   *  Speichergrösse: `2048 MB`
   *  Platte:         `[X] Festplatte erzeugen`
4. Auf `Erzeugen` klicken
5. Weiteres Fenster öffnet sich, folgende Informationen eintragen:
   *  Dateipfad:                       standard
   *  Dateigrösse:                     `10.00 GB`
   *  Dateityp der Festplatte:         `VMDK (Virtual Maschine Disk)`
   *  Storage on physical hard disk:   `dynamisch alloziert`
6. Ebenfalls auf `Erzeugen` klicken, dann im Hauptmenü die VM anwählen (blau markiert) und den Punkt `Ändern` aufrufen
7. Im Abschnitt `Massenspeicher` den SATA-Controller anwählen und auf das CD+Symbol klicken
8. Unter `Medium auswählen` das zuvor heruntergeladene Systemabbild (ISO-Datei) anwählen
9. Alle Änderungen speichern und die VM starten
10. Den Installationsanweisungen der OS-Installation folgen und anschliessend zu Abschnitt "VM einrichten" gehen

### VM einrichten

Als nächstes installiert man ein Webserver. 

1. Ubuntu-VM starten
2. Anmelden und Terminal (*Bash*) öffnen
3. Paketliste neu einlesen und Pakete aktualisieren:
   ```Shell 
   $  sudo apt-get update   #Paketlisten des Paketmanagement-Systems "APT" neu einlesen
   
   $  sudo apt-get upgrade   #Installierte Pakete wenn möglich auf verbesserte Versionen aktualisieren

   $  sudo reboot           #System-Neustart durchführen
   ```
4. Software Controlcenter "Synaptic" installieren:
   ```Shell 
   $  sudo apt-get install synaptic
   ```
5. Nach erfolgreicher Installation in der Suche nach "Synaptic Package Manager" suchen und diesen starten
6. Innerhalb des Managers nach "apache" (Webserver-Programm) suchen und dieses (inkl. aller Abhängigkeiten) installieren
7. System-Neustart durchführen:
   ```Shell 
   $  sudo reboot
   ```
8. Gängiger Web-Browser (z.B. Firefox) starten und prüfen, ob der Standard-Content des Webservers unter "http://127.0.0.01:80" (localhost) erreichbar ist
9. Browser-Fenster schliessen und VM wieder herunterfahren/stoppen

## Vagrant
Zuerst habe ich Vagrant auf der Webseite "www.vagrantup.com"   heruntergeladen und GUI-Basiert installiert.

*Danach habe ich mit Vagrant eine VM erstellt.*
1. Terminal öffnen
2. Einen neuen Ordner für die VM anlegen:
    Shell
      $ cd C:\Users\Besar
      $ mkdir MeineVagrantVM
      $ cd MeineVagrantVM
     
3. Vagrantfile erzeugen, VM erstellen und starten:
    ```Shell
      $ vagrant box add http://10.1.66.11/vagrant/ubuntu/xenial64.box --name ubuntu/xenial64  #Vagrant-Box vom Netzwerkshare hinzufügen
      $ vagrant init ubuntu/xenial64        #Vagrantfile erzeugen
      $ vagrant up --provider virtualbox    #Virtuelle Maschine erstellen & starten
     ```
4. Die VM ist nun bereit und kann mit SSH-Zugriff bedient werden:
    ```Shell
      $ cd C:\Users\Besar\MeineVagrantVM      #Zum Verzeichnis der VM wechseln
      $ vagrant ssh                       #SSH-Verbindung zur VM aufbauen
      ```
### Vm erstellen mit abgeändertem File
1. Terminal öffnen
2. In das Verzeichnis wechseln, wo das Vagrantfile ist:
    ```Shell
      $ cd C:\Users\Besar\M300\vagrant\web
     ```
3. VM erstellen und starten:
    ```Shell
      $ vagrant up
     ```
4. Danach habe ich im Webbrowser geprüft, ob der Standard-Content des Webservers unter "http://127.0.0.01:8080" (localhost) erreichbar ist
5. Später habe ich im Ordner `\web` die Hauptseite `index.html` editiert und das Resultat überprüft.
6. Abschliessend habe ich die VM wieder gelöscht:
    Shell
      $ vagrant destroy -f
## Visualstudio-Code
1. Ich habe Visual Studio Code auf derWebseite "code.visualstudio.com" heruntergelden und GUI-basiert installiert.
2. Danach habe ich dem Editor drei wichtige Extensions hinzugefügt:
3. Einstellungen angepasst.

* Markdown All in One (von Yu Zhang)
* Vagrant Extension (von Marco Stanzi)
* vscode-pdf Extension (von tomiko1207)

Dazu habe ich folgende Anweisungen befolgt: 

  1. Visual Studio Code öffnen
  2. In der Suchleiste die erwähnten Extensions suchen
  3. Auf `Install` klicken und anschliessend auf `Reload`, um die Extension in den Arbeitsbereich zu laden.
  4. Unten links auf "Settings" und auf "Add Pattern" die Richtigen Pattern hinzugefügt.
   
Danach habe ich 
*Um die Dokumentation lokal mit Visual Studio Code zu bearbeiten, arbeite ich folgendermassen:*

  1. Änderungen am Readme-File von meinem Repositorys vornehmen
  2. Datei speichern und in der linken Leiste das Symbol mit einer "1" aufrufen
  3. Unter dem Abschnitt *Changes* die betroffenen Files bezüglich ihres Changes "stagen"
  4. Nachricht hinterlegen und Haken setzen
  5. Bei den 3 Punkten (...) auf *Push* klicken
  6. Warten, bis Dateien vollständig gepusht wurden

## Git-Client

Damit ich die Arbeiten lokal auf dem eigenen PC machen konnte, musste ich der sogenannte "Git Client", auf Windows "Git/Bash" installieren. 

*Client installieren*
Ich habe Client-Installation auf https://git-scm.com/downloads heruntergeladen und GUI-basiert installiert.

*Danach habe ich den Client konfiguriert:*
1. Terminal öffnen
2. Git konfigurieren mit Informationen des GitHub-Accounts:
    Shell
      $ git config --global user.name "<username>"
      $ git config --global user.email "<e-mail>"
     

*Damit ich das readme-File lokal bearbeiten kann, habe ich das Repository heruntergeladen und aktualisiert.*

1. Terminal öffnen
2. Ordner für Repository erstellen:
    Shell
      $ cd C:\Users\besar\Desktop
      $ mkdir githublb2
     
3. Repository mit SSH klonen:
    Shell
      $ git clone git@github.com:besarsabani/lb2.git

      Cloning into 'lb2'...
     
4. Repository aktualisieren und Status anzeigen:
    Shell
      $ git pull

      Already up to date.
## ssh-Key

*Zuerst musste ich Lokal einen SSH-Key erstellen:*

1.  Folgenden Befehl mit der Account-E-Mail von GitHub in Bash einfügen:
    Shell
      $  ssh-keygen -t rsa -b 4096 -C "beaarsabani00@gmail.com"
    
2. Neuer SSH-Key wird erstellt:
    Shell
      Generating public/private rsa key pair.
    
3. Bei der Abfrage, unter welchem Namen der Schlüssel gespeichert werden soll, die Enter-Taste drücken (für Standard):
    Shell
      Enter a file in which to save the key (~/.ssh/id_rsa): [Press enter]
    
4. Nun habe ich ein Passwort für den Key festgelegt:
    Shell
      Enter passphrase (empty for no passphrase): [Passwort]
      Enter same passphrase again: [Passwort wiederholen]
    
*Danach kann ich den SSH-Key dem Client hinzufügen:*
1. Auf www.github.com im Benutzerkonto *Settings* aufrufen
2.  Unter den Menübereichen auf der linken Seite zum Abschnitt *SSH und GPG keys* wechseln
3.  Auf *New SSH key* klicken
4.  Im Formular unter *Title* die Bezeichnung MB SSH-Key vergeben
5.  Den Key von der Datei *C:\Users\besar\.ssh\id_rsa.pub* einfügen und auf *Add SSH key* klicken

*SSH Zugriff auf VM*

Um Zugriff via SSH auf die VM aufzubauen, muss man bloss einen kurzen Befehl eingeben.
shell
vagrant ssh

K2
======
> [⇧ *Nach oben*](#inhaltsverzeichnis)
## GitHub Account

*Ich habe folgendermassen einen Github Account erstellt:*
1. Auf [GitHub.com](https://github.com) gehen
2. Auf *Sign up* klicken
3. Username, E-mail und Passwort eingeben sowie Aufgabe zum verifizieren lösen
4. Auf *Create an Account* klicken

K3
======

> [⇧ *Nach oben*](#inhaltsverzeichnis)
 
## Testen

### Apache
- Ich habe den Apache getestet, indem ich auf meinem Client die IP-Adresse der VM eingegeben habe. 
- Zudem habe ich das index.html geändert und geschaut ob es die Änderungen übernommen hat.

### Users-and-Groups
- Mit diesem Befehl habe ich alle Benutzer in der VM angezeigt und habe dann gesehen, das meine beiden User erstellt worden sind.
    Shell
    cut -d: -f1 /etc/passwd
    
- Mit diesem Befehl zeige ich die Gruppen in der VM an und sehe dann, ob die neue Group erstellt wurde.
    Shell
    cut -d: -f1 /etc/group
    
-  Die beiden Befehle oben kann man in einen zusammenfassen, indem man den User mit der dazugehörigen Group anzeigt:
    Shell
    cut -d: -f1 /etc/passwd | xargs groups
    

- Um zu testen, ob das Passwort geändert wurde, habe ich mich mit einem zuvor erstellten User eingeloggt.
    Shell
    su user01
    password: ****
    

### Ports
- Um zu testen, ob es die Portkonfiguration übernommen hat,    habe ich folgenden Befehl eingegeben und gesehen, dass die im File angegebenen Ports offen sind.
    Shell
    netstat -an |grep LISTEN 
    
- In diesem Fall habe ich Port 80 für die Webseite und Port 22 für die SSH-Verbindung geöffnet. Dies kann man auch testen, indem man die Webseite aufruft und eine Verbindung via SSH aufbaut. 

K4
======

> [⇧ *Nach oben*](#inhaltsverzeichnis)
 
## Firewall

  *Ich habe beim aufsetzen automatisch Firewall Regeln erstellt, indem ich die nötigen Zeilen ins Vagrantfile eingefügt habe:*

1. Vagrantfile öffnen
2. Folgende Zeilen einfügen:
    Shell
      sudo apt-get install ufw
      sudo ufw allow 80/tcp
      sudo ufw allow 22/tcp
      sudo ufw allow out 22/tcp 
      sudo ufw enable
     
## Benutzer-und-Rechtevergabe

*Ich habe beim aufsetzen automatisch User mit Passwort erstellt, indem ich die nötigen Zeilen ins Vagrantfile eingefügt habe:*

1. Vagrantfile öffnen
2. Folgende Zeilen einfügen:
    Shell
      sudo groupadd testadmin
      sudo useradd user1 -g testadmin -m -s /bin/bash 
      sudo useradd user2 -g testadmin -m -s /bin/bash 
      sudo chpasswd <<<user1:abc123	
      sudo chpasswd <<<user2:abc123
    
## SSH

*Ich habe beim aufsetzen automatisch ein SSH Zugang erstellt, indem ich die nötigen Zeilen ins Vagrantfile eingefügt habe:*

1. Vagrantfile öffnen
2. Folgende Zeilen einfügen:
    Shell
      sudo apt-get -y install openssh-server
    

K5
======

> [⇧ *Nach oben*](#inhaltsverzeichnis)
 

## Vergleich Vorwissen - Wissenszuwachs

*Bereits bekannt*

- Die manuelle Virtualisierung von Ubuntu habe ich schon öfters in anderen Modulen oder im ÜK gemacht.

*Neu*

 - Vor diesem Modul habe ich immer mit VMWare gearbeiet, also war VirtualBox neu für mich. Ich bin aber sehr schnell und gut zurecht gekommen, da es keine grossen Unterschiede zwischen den beiden gibt.
 - Ich kannte Vagrant vor diesem Modul nicht, daher war alles davon neu für mich.
 - Auch mit Markdown bin ich zuvor nicht in Berührug gekommen.

*Fazit*

Ich konnte sehr von LB2 provitieren, da vieles neu für mich war. Vor allem Vagrant und Markdown konnte ich viel neues lernen, da ich zuvor noch nie etwas damit zu tun hatte.

## Reflexion

Ich habe bei der LB2 mehr Zeit in die Dokumentation gesteckt, wie in die eigentliche Arbeit. Da wir die Funktionen, die in LB2 automatisert werden müssen, schon beim Teil 10 manuell gemacht haben, konnte man vieles wiederholen. Einzig die Anpassungen im Vagrantfile sind neu dazugekommen. Wobei man sagen muss, dass die meissten Befehle, die darin eingebaut werden, ebenfalls schon bei Teil 10 vorgekommen sind. Die Dokumentation mit Markdown war, wie schon erwähnt neu für mich und hat daher die meisste Zeit in anspruch genommen..

# LB3-Docker

## K1-LB3

Da ich für die LB2 die Umgebung schon eingerichtet habe und diese Dokumentiert habe, Kommt man mit diesem Link zu dieser Kompetez.
> [⇧ *Zur Umgebungs Doku*](#K1)

## K2-LB3

Für die LB2 musste ich auch hier diese Kompetenzen erfüllen. Mit diesem Link kommt man auf die richtige Doku
> [⇧ *Zur Umgebungs Doku*](#K1)

> [⇧ *Zur Git-client Anleitung*](#K2)

## Vorwissen zu Docker

Ich habe zuvor noch nie mit Docker gearbeitet. Im Geschäft hatte ich noch nichts mit Docker zutun. In diesem Modul habe ich vieles über Docker gelernt. Die LB2 über Vagrant hat mir sehr geholfen, um Docker zu verstehen. Die Dokus im Git haben mir ebenfall sehr geholfen. Ich habe auch die Docker Hub webseite angeschaut. 

<https://docs.docker.com/get-started>

## K3-Docker

### Docker Container
Ich habe ein Dockerfile und ein Docker-Compose erstellt. 

Im Dockerfile werde ich ein Webserver und eine Mysql Datenbank installieren. 
Im Compose-File ist die Config drauf. Dari werde ich ein PHPadmin entsprechend einrichten.

Im Docker file habe ich folgende 2 Zeilen hinzugefügt um die php extension hinzuzufügen:
1. FROM php:7.1-apache
2. RUN docker-php-ext-install mysqli

Im Compose file habe ich folgende zeilen für Webserver und PHP config:
```Shell
php:
    build: php
    ports:
      - "80:80"
      - "443:443"k
    restart: on-failure
    volumes:
      - .besar/test:/var/www/html
    cpus: 1
    mem_limit: 1024m
```
Hier der Code für den Graphischen Mysql zugriff.
```Shell
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    links:
        - db:db
    ports:
        - 8080:80
    restart: on-failure
    environment:
        MYSQL_ROOT_PASSWORD: dockerischlustig
    cpus: 1
    mem_limit: 1024m
```
Hier der Code für den Mysqlserver
```Shell
  db:
    image: mysql:5.7
    ports:
     - "3306:3306"
    volumes:
     - /var/lib/mysql
    restart: on-failure
    environment:
     - MYSQL_ROOT_PASSWORD=dockerischlustig
     - MYSQL_DATABASE=database
    cpus: 1
    mem_limit: 1024m
```
### Backend-Frontend

Als Frontend habe ich PHP eingerichtet und als Backend den Mysql server, der im Hintergrung läuft.

### Volumes für Datenablage

Hier habe ich beim PHP den Pfad angegeben, bei dem der Docker auf mein Index.html zugreift. Wenn ich dieses File Lokal anpasse, wird das File im Docker automatisch angepasst und die Webseite aktualisiert.

### Docker Spezifische Befehle

Hier eine Auflistung der wichtigsten Docker Befehle:

```Shell
$ #Docker file erstellen
$ docker build -t name .
$ #startet name und mappt port 4000 zu 80
$ docker run -p 4000:80 name
$ #Listet alle Container auf
$ docker container ls -a
$ # Stoppt Container
$ docker container stop <hash>
$ #Force Shutdown
$ docker container kill <hash>
$ # Löscht container
$ docker container rm <hash>
$ # List images
$ docker image ls -a
$ # Löscht Image
$ docker image rm <image id>
$ # Docker compose starten
$ docker-compose up
```
## Funktion

Ich habe die Funktion der Docker ebenfalls geprüft. Folgende Testfälle habe ich Dokumetiert.

| **Test Punkt**                                               | **Erwartetes Ergenis**                                       | **Tatsächliches Ergebnis** |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------------- |
| Webserver erreichbar unter localhost                         | Index file seite wird angezeigt| Funktioniert!              |
| MySQL über Phpmyadmin erreichbar                             | PhpMyAdmin login funktioniert mit MySQL Env-Variabeln        | Funktioniert!              |
| Webserver Anpassungen werden übernommen | Nach dem Anpassen des Index files ist die Webseite uch direkt angepasst | Funktioniert!              |


## Sicherheit

### Image Poisoning
Die Images habe ich nur von der Offiziellen Docker hub Seite herunterladen.  

### Ressourcen Limiten angeben
Cpu und Memory Limiten erstellen, damit der Docker nicht unnötige Ressourcen braucht. Ebenfalls kann man Einrichten, dass man bei grosser Last eine Benachrichtigung bekommt und das Problem so Analysiert.

### Benachrichtungen
Man kann bei prtg trigger erstellen wenn eine Benachrichtigung erscheinen soll. Man kann z.b trigger erstellen wenn alle Ressourcen gebraucht werden, oder wenn etwas verändert wurde.