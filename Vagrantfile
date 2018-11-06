# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "acs" do |acs|
  acs.vm.box = "centos/7"
  acs.vm.network "forwarded_port", guest: 80, host: 8080
  acs.vm.network "private_network", ip: "192.168.33.10"
  acs.vm.hostname = "acs"
  acs.vm.provision "shell", inline: <<-SHELL
    yum -y update
    yum install -y nano vim
    yum -y install ansible
    sudo echo "192.168.33.10 acs" | sudo tee -a /etc/hosts
    sudo echo "192.168.33.100 lb" | sudo tee -a /etc/hosts
    sudo echo "192.168.33.20 web1" | sudo tee -a /etc/hosts
    sudo echo "192.168.33.30 web2" | sudo tee -a /etc/hosts
    sudo echo "192.168.33.40 db01" | sudo tee -a /etc/hosts
    sed -i "s/^PasswordAuthentication no/PasswordAuthentication yes/" /etc/ssh/sshd_config
    systemctl restart sshd
  SHELL
  end


  config.vm.define "lb" do |lb|
  lb.vm.box = "centos/7"
  lb.vm.network "private_network", ip: "192.168.33.100"
  lb.vm.hostname = "lb"
  config.vm.provider "virtualbox" do |vb|
  	vb.memory = "256"
  end	
  lb.vm.provision "shell", inline: <<-SHELL
    yum -y update
    yum install -y nano vim
    sudo echo "192.168.33.10 acs" | sudo tee -a /etc/hosts
    sudo echo "192.168.33.100 lb" | sudo tee -a /etc/hosts
    sudo echo "192.168.33.20 web1" | sudo tee -a /etc/hosts
    sudo echo "192.168.33.30 web2" | sudo tee -a /etc/hosts
    sudo echo "192.168.33.40 db01" | sudo tee -a /etc/hosts
    sed -i "s/^PasswordAuthentication no/PasswordAuthentication yes/" /etc/ssh/sshd_config
    systemctl restart sshd
  SHELL
 end

  config.vm.define "web1" do |web1|
  web1.vm.box = "centos/7"
  web1.vm.network "forwarded_port", guest: 80, host: 8081
  web1.vm.network "private_network", ip: "192.168.33.20"
  web1.vm.hostname = "web1"
  config.vm.provider "virtualbox" do |vb|
  	vb.memory = "256"
  end	
  web1.vm.provision "shell", inline: <<-SHELL
    yum -y update
    yum install -y nano vim
    sed -i "s/^PasswordAuthentication no/PasswordAuthentication yes/" /etc/ssh/sshd_config
    systemctl restart sshd
  SHELL
 end

  config.vm.define "web2" do |web2|
  web2.vm.box = "centos/7"
  web2.vm.network "forwarded_port", guest: 80, host: 8082
  web2.vm.network "private_network", ip: "192.168.33.30"
  web2.vm.hostname = "web2"
  config.vm.provider "virtualbox" do |vb|
  	vb.memory = "256"
  end	
  web2.vm.provision "shell", inline: <<-SHELL
    yum -y update
    yum install -y nano vim
    sed -i "s/^PasswordAuthentication no/PasswordAuthentication yes/" /etc/ssh/sshd_config
    systemctl restart sshd
  SHELL
 end

  config.vm.define "db01" do |db01|
  db01.vm.box = "centos/7"
  db01.vm.network "private_network", ip: "192.168.33.40"
  db01.vm.hostname = "db01"
  config.vm.provider "virtualbox" do |vb|
  	vb.memory = "256"
  end	
  db01.vm.provision "shell", inline: <<-SHELL
    yum -y update
    yum install -y nano vim
    sed -i "s/^PasswordAuthentication no/PasswordAuthentication yes/" /etc/ssh/sshd_config
    systemctl restart sshd
  SHELL
 end
end
