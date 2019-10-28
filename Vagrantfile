# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  
  config.vm.define "dev", primary: true do |dev|
    dev.vm.network "private_network", ip: "172.28.128.10"
    dev.vm.hostname = "share-space-dev"
  end

  config.vm.define "prod", autostart: false do |prod|
    prod.vm.network "private_network", ip: "172.28.128.11"
    prod.vm.hostname = "share-space-prod"
  end

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "8192"
    vb.cpus = 8
  end

  config.vm.provision "install", type: "shell", privileged: false, path: "install"
  config.vm.provision "stack-up", type: "shell", privileged: false, run: "never", path "stack-up"
  config.vm.provision "stack-down", type: "shell", privileged: false, run: "never", path "stack-down"
end
