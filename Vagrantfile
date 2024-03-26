# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/jammy64"
  
  config.vm.define "lab1" do |subconfig|
      subconfig.vm.box = "ubuntu/jammy64"
      subconfig.vm.hostname="lab1"
      subconfig.vm.network "private_network", ip: "192.168.0.10",virtualbox__intnet: true,virtualbox__intnet:"intneta"
      subconfig.vm.network "private_network",ip: "192.168.2.10",virtualbox__intnet: true,virtualbox__intnet:"intnetb"
      subconfig.vm.network "forwarded_port", guest: 22, host: 20001, host_ip: "127.0.0.1"
      subconfig.vm.network "forwarded_port", guest: 8080, host: 8080
      subconfig.vm.provider :virtualbox do |vb|
         # Custom CPU & Memory
         vb.customize ["modifyvm", :id, "--memory", "1024"]
         vb.customize ["modifyvm", :id, "--cpus", "1"]
      end
      subconfig.vm.provision "shell", inline: <<-SHELL
      sudo echo "192.168.0.11 lab2" | sudo tee -a /etc/hosts
      sudo echo "192.168.2.11 lab3" | sudo tee -a /etc/hosts
      sudo apt update
      sudo apt install net-tools
        SHELL
  end
  
  config.vm.define "lab2" do |subconfig|
      subconfig.vm.box = "ubuntu/jammy64"
      subconfig.vm.hostname="lab2"
      subconfig.vm.network "private_network", ip: "192.168.0.11",virtualbox__intnet: true,virtualbox__intnet:"intneta"
      #subconfig.vm.network "private_network",ip: "192.168.2.1",virtualbox__intnet: true,virtualbox__intnet:"intnetb"
      subconfig.vm.network "forwarded_port", guest: 22, host: 20002, host_ip: "127.0.0.1"
      subconfig.vm.provider :virtualbox do |vb|
         # Custom CPU & Memory
         vb.customize ["modifyvm", :id, "--memory", "1024"]
         vb.customize ["modifyvm", :id, "--cpus", "1"]
      end
      subconfig.vm.provision "shell", inline: <<-SHELL
      sudo echo "192.168.0.10 lab1" | sudo tee -a /etc/hosts
      sudo echo "192.168.2.11 lab3" | sudo tee -a /etc/hosts
      sudo apt update
      sudo apt install net-tools
        SHELL
  end
  
  config.vm.define "lab3" do |subconfig|
    subconfig.vm.box = "ubuntu/jammy64"
    subconfig.vm.hostname="lab3"
    subconfig.vm.network "private_network", ip: "192.168.2.11",virtualbox__intnet: true,virtualbox__intnet:"intnetb"
    #subconfig.vm.network "private_network",ip: "192.168.2.1",virtualbox__intnet: true,virtualbox__intnet:"intnetb"
    subconfig.vm.network "forwarded_port", guest: 22, host: 20003, host_ip: "127.0.0.1"
    subconfig.vm.provider :virtualbox do |vb|
       # Custom CPU & Memory
       vb.customize ["modifyvm", :id, "--memory", "1024"]
       vb.customize ["modifyvm", :id, "--cpus", "1"]
    end
    subconfig.vm.provision "shell", inline: <<-SHELL
    sudo echo "192.168.2.10 lab1" | sudo tee -a /etc/hosts
    sudo echo "192.168.0.11 lab2" | sudo tee -a /etc/hosts
    sudo apt update
    sudo apt install net-tools
      SHELL
end
end
 

