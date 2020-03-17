## Webserver
``` 
+-------------------------------+      
! VM1: Ubuntu                   ! 
+ Port: Gast:80 Host:8080       +       
! Arbeitsspeicher: 1024 MB      !	    
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
#Zeile 33: Jedes Vagrantfile beginnt mit dieser Zeile. Die zwei definiert die Version.

Vagrant.configure("2") do |config|


# Zeile 44: Hier beginnt die Definition der Ubuntu VM.
# Zeile 45: Das ist eine Vagrantbox, welches die Ubuntu Version 16.04 enthält.
# Zeile 46: Hier wird die Portweiterleitung definiert.
# Zeile 47: Hier wird der Pfad "/var/www/html" in der Ubuntu VM erstellt
# Zeile 48: Hier geben ich an das ich Virtualbox als Infrastruktur für meine VM möchte.
# Zeile 49: Der VM habe ich einen GB an RAM gegeben.
# Zeile 50: Die Definition der Virtualbox beende ich mit dieser Zeile.

  config.vm.define "ubuntu" do |ubu|
      ubu.vm.box = "ubuntu/xenial64"
      ubu.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
      ubu.vm.synced_folder ".", "/var/www/html"  
      config.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"  
      end
      

# Zeile 60: Hier beginnt die Provision Definition mit Shell-Befehlen.
# Zeile 50: Hier wird das allgemeine Update durchgeführt.
# Zeile 51: Hier wird Apache installiert.
# Zeile 52: Hiermit werden die Shell-Befehle eingegrenzt.
# Zeile 53: Hiermit endet die Konfiguration der Provision.
# Zeile 54: Hiermit endet die Konfiguration der Vagrantdatei.

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get -y install apache2 
      SHELL
  end
end
```

___
### Test
[x] Die konfigurierte Maschinen starten ohne Fehlermeldung.
[x] Alle im Vagrantfile definierte Konfigurationen werden ausgeführt.
[x]Wenn man localhost:8080 anfragt, wird die Defaultseite von Apache dargestellt.
___
### Quellen
- https://github.com/mc-b/M300/tree/master/vagrant/web
