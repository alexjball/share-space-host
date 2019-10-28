# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  
  config.vm.define "dev", primary: true do |dev|
    dev.vm.network "private_network", ip: "172.28.128.10"
    dev.vm.hostname = "share-space-dev"
    dev.vm.provision ".devrc", type: "file", source: ".devrc", destination: "~/.deploymentrc"
  end

  config.vm.define "prod", autostart: false do |prod|
    prod.vm.network "private_network", ip: "172.28.128.11"
    prod.vm.hostname = "share-space-prod"
    prod.vm.provision ".prodrc", type: "file", source: ".prodrc", destination: "~/.deploymentrc"
  end

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "site", "/home/vagrant/site",  create: true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = 4
  end

  config.vm.provision "stack-install", type: "shell", privileged: false,               path: "run-env", args: "stack-install"
  config.vm.provision "stack-build",   type: "shell", privileged: false, run: "never", path: "run-env", args: "stack-build"
  config.vm.provision "stack-up",      type: "shell", privileged: false, run: "never", path: "run-env", args: "stack-up"
  config.vm.provision "stack-down",    type: "shell", privileged: false, run: "never", path: "run-env", args: "stack-down"
  config.vm.provision "stack-status",  type: "shell", privileged: false, run: "never", path: "run-env", args: "stack-status"
end
