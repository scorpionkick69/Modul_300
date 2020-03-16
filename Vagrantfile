# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "lb1" do |lb1|
    lb1.vm.box = "ubuntu/trusty64"
    lb1.vm.network "private_network", ip: "192.168.5.10"
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"  
    end
    
    lb1.vm.provision "shell", path: "provision-lb.sh"
    end

  config.vm.define "web1" do |web1|
    web1.vm.box = "ubuntu/trusty64"
    web1.vm.network "private_network", ip: "192.168.5.11"
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"  
    end

    web1.vm.provision :shell do |shell|
          shell.args = "1"
          shell.path = "provision-web.sh"
    end
  end

  config.vm.define "web2" do |web2|
    web2.vm.box = "ubuntu/trusty64"
    web2.vm.network "private_network", ip: "192.168.5.12"
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"  
    end

    web2.vm.provision :shell do |shell|
          shell.args = "2"
          shell.path = "provision-web.sh"
    end
  end

  config.vm.define "ubuntu" do |ubu|
    config.vm.box = "ubuntu/xenial64"
    config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
    config.vm.synced_folder ".", "/var/www/html"  
    config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"  
    end
  config.vm.provision "shell", inline: <<-SHELL
    # Packages vom lokalen Server holen
    # sudo sed -i -e"1i deb {{config.server}}/apt-mirror/mirror/archive.ubuntu.com/ubuntu xenial main restricted" /etc/apt/sources.list 
    sudo apt-get update
    sudo apt-get -y install apache2 
  SHELL
  end
end
