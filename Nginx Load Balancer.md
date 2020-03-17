## Nginx Load Balancer
``` 
+-------------------------------+       +-------------------------------+
! VM1: Load Balancer            !	      ! VM2: Webserver                !
+ Privates Netz: 192.168.5.10   +       + Privates Netz: 192.168.5.11   +
! Arbeitsspeicher: 1024 MB      !       ! Arbeitsspeiche: 1024 MB       !
+ Provision: provision-lb.sh    +       + Provision: provision-web.sh   !
+-------------------------------+       +-------------------------------+
+-------------------------------+  
! VM3: Webserver                !
+ Privates Netz: 192.168.5.12   +
! Arbeitsspeicher: 1024 MB      !
+ Provision: provision-web.sh   + 
+-------------------------------+
```
1.) Vagrantfile lokal speichern
2.) Den Code nach eigenem Wunsch anpassen
### Entweder ein privates Netzwerk einrichten
```
lb1.vm.network "private_network", ip: "192.168.5.10"
```
### Oder eine Portweiterleitung einrichten
```
config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
```
3.) Vagrantdatei in Git Bash ausführen (Der Webserver läuft über Virtualbox.)
```
cd c:/Users/amirthalingamp/Modul_300
vagrant up
```

4.) Die Apache Default Seite ist entweder über das privat eingerichtete Netzwerk erreichbar. Dazu gibt man im Browser die IP ein Bsp. 192.168.5.10. Wenn man die Portweiterleitung eingerichtet hat, gibt man im Browser beispielsweise http://localhost:8080 ein.
___

## Code
```
#Zeile 39: Jedes Vagrantfile beginnt mit dieser Zeile. Die zwei definiert die Version

Vagrant.configure("2") do |config|              


# Zeile 49: Hier beginnt die Definition der Load Balancer VM
# Zeile 50: Das ist eine Vagrantbox, welches die Ubuntu Version 14.04 enthält.
# Zeile 51: Hier wird die IP des Load Balancer definiert.
# Zeile 52: Hier gebe ich an das Virtualbox die Infrastruktur ist für meine VM.
# Zeile 53: Der VM habe ich einen GB an RAM gegeben.
# Zeile 54: Die Definition der Virtualbox beende ich mit dieser Zeile.

  config.vm.define "lb1" do |lb1|               
    lb1.vm.box = "ubuntu/trusty64"              
    lb1.vm.network "private_network", ip: "192.168.5.10"    
    config.vm.provider "virtualbox" do |vb|     
    vb.memory = "1024"                          
    end                                         
 
 
 # Zeile 60: Hier verweise ich auf mein Provision-File. Wenn man auf die IP vom Load Balancer zugreift, wird Anfrage zu einem von den zwei Webserver weitergeleitet.
 # Zeile 61: Diese Datei ist für den Load Balancing der zwei anderen Maschinen zuständig   
 
    lb1.vm.provision "shell", path: "provision-lb.sh" 
    end                            


# Zeile 70: Hier beginnt die Definition des ersten Webservers.
# Zeile 71: Hier nutzte ich die gleiche Vagrantbox wie für lb1, man kann auch eine andere nutzen.
# Zeile 72: Hier wird die IP des Webservers definiert.
# Zeile 73: Hier gebe ich an das Virtualbox die Infrastruktur ist für meine VM.
# Zeile 74: Der VM habe ich einen GB an RAM gegeben.
# Zeile 75: Die Definition der Virtualbox beende ich mit dieser Zeile.

  config.vm.define "web1" do |web1|             
    web1.vm.box = "ubuntu/trusty64" 
    web1.vm.network "private_network", ip: "192.168.5.11"
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"  
    end


# Zeile 85: Hier wird die Provisiondatei vom Webserver1 definiert
# Zeile 86: Web 1 wird das Argument 1 gegeben, wenn man auf den Load Balancer anfragt, wird der Webserver1 als erstes angefragt.
# Zeile 87: Es soll die Shelldatei "provision-web" ausgeführt werden.
# Zeile 88: Shell-Definition endet hier.
# Zeile 89: Die Definition des Webserver1 endet hier.

    web1.vm.provision :shell do |shell|
          shell.args = "1"
          shell.path = "provision-web.sh"
    end
  end

# Zeile 98: Hier beginnt die Definition des zweiten Webservers.
# Zeile 99: Hier nutzte ich die gleiche Vagrantbox wie für lb1, man kann auch eine andere nutzen.
# Zeile 100:Hier wird die IP des Webservers definiert.
# Zeile 101:Hier gebe ich an das Virtualbox die Infrastruktur ist für meine VM.
# Zeile 102:Der VM habe ich einen GB an RAM gegeben.
# Zeile 103:Die Definition der Virtualbox beende ich mit dieser Zeile.

  config.vm.define "web2" do |web2|
    web2.vm.box = "ubuntu/trusty64"
    web2.vm.network "private_network", ip: "192.168.5.12"
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"  
    end


# Zeile 113:Hier wird die Provisiondatei vom Webserver2 definiert und zudem angegeben, dass der Befehl zwischen 114 und 116 als Shell-Befehl ausgeführt werden muss
# Zeile 114: Web2 wird das Argument 2 gegeben. Wenn der Web1 beschäftigt ist, wird die nächste Anfrage über Web2 durchgeführt.
# Zeile 115:Es soll die Shelldatei "provision-web" ausgeführt werden. Hier wird definiert, dass die Default HTML-Seite angezeigt wird.
# Zeile 116:Shell-Definition endet hier
# Zeile 117:Die Definition des Webserver1 endet hier.
# Zeile 118:Die Definition der ganzen Vagrantdatei endet hier.

    web2.vm.provision :shell do |shell|
          shell.args = "2"
          shell.path = "provision-web.sh"
    end
  end
 end
```

___
### Test
[x] Die konfigurierte Maschinen starten ohne Fehlermeldung.
[x] Alle im Vagrantfile definierte Konfigurationen werden ausgeführt.
[x]Wenn man den Load Balancer anfragt, wird der Web1 antworten.
[x]Wenn man die Seite neu lädt, wird antwortet der andere Server.
___
### Quellen
- https://www.youtube.com/watch?v=aHwFKTHdKX8
