# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update

    # install git
    apt-get install -y git

    # install pip
    wget https://bootstrap.pypa.io/get-pip.py
    python get-pip.py

    # install ansible and docker-py
    pip install ansible docker

    # install docker
    curl -fsSL get.docker.com -o get-docker.sh
    sudo sh get-docker.sh

    # install awx
    # git clone https://github.com/ansible/awx.git
    # git checkout 1.0.1
    cd /vagrant/installer
    ansible-playbook -i inventory install.yml
  SHELL
end
