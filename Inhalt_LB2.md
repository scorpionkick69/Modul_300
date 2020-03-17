# Modul 300 Dokumentation Amirthalingam
``` 
+---------------------------------------------------------------+
! Autor: Piravis Amirthalingam                                  !	
+---------------------------------------------------------------+
! Datum: 15.03.2020                                             !	
+---------------------------------------------------------------+
! Modul: 300/LB2                                                !	
+---------------------------------------------------------------+
! Version: 1                                                    !	
+---------------------------------------------------------------+
```
## Inhalt
1. [Einleitung](#Einleitung)
2. [Vorbereitung](#Vorbereitung)
3. [Nginx Load Balancer](#Nginx)
4. [Webserver](#Webserver)
5. [Test](#Test)
6. [Quellen](#Quellen)
___
### Einleitung
Meine Dokumentation enthält:
- Ein Nginx Load Balancer, der aus einem Load Balancer und zwei Webservern besteht
- Einen einfachen Apache-Webserver
 ___
### Vorbereitung
- Mein Repository auf die lokale Festplatte clonen
```
git clone https://github.com/scorpionkick69/Modul_300.git
```
- In diesem Verzeichnis Git Bash starten
___
### Nginx Load Balancer
Vagrantdatei vom Nginx Load Balancer ist unter diesen Link vorhanden:
https://github.com/scorpionkick69/Modul_300/blob/master/Vagrantfile_Nginx

Die Dokumentation über den Load Balancer ist unter diesen Link vorhanden:
https://github.com/scorpionkick69/Modul_300/blob/master/Nginx_Load_Balancer.md
___
### Webserver
Vagrantdatei vom Webserver ist unter folgenden Link vorhanden:
https://github.com/scorpionkick69/Modul_300/blob/master/Vagrantfile_Webserver

Die Dokumentation über den Webserver ist unter folgenden Link vorhanden:
https://github.com/scorpionkick69/Modul_300/blob/master/Webserver.md
___
### Test
[x] Die konfigurierte Maschinen starten ohne Fehlermeldung.
[x] Alle im Vagrantfile definierte Konfigurationen werden ausgeführt.
[x] Wenn man localhost:8080 anfragt, wird die Defaultseite von Apache dargestellt.
[x] Wenn man den Load Balancer anfragt, wird der Web1 als erstes antworten.
___
### Quellen
- https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet
- https://github.com/mc-b/M300/tree/master/vagrant/web
- https://www.youtube.com/watch?v=aHwFKTHdKX8