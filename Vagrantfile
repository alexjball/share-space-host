# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  
  # Environment definitions using Vagrant multi-machine features.
  # To add an environment:
  # - Add a define block with the name and hostname of the environment
  # - Assign an unused IP to the environment. IP's in this file are based
  #   on the default VirtualBox private network.
  # - (optional) Add a line to /etc/hosts mapping the env IP to its hostname.
  #   this allows accessing the env locally by its hostname rather than IP.
  # - Add a provisioner for the environment's envrc to define env-specific
  #   variables.

  config.vm.define "dev", primary: true do |dev|
    dev.vm.network "private_network", ip: "172.28.128.10"
    dev.vm.hostname = "share-space-dev"
    if (File.file?(".devrc"))
      dev.vm.provision ".devrc", type: "file", source: ".devrc", destination: "~/.deploymentrc"
    end
  end

  config.vm.define "staging", primary: true do |dev|
    dev.vm.network "private_network", ip: "172.28.128.12"
    dev.vm.hostname = "share-space-staging"
    if (File.file?(".stagingrc"))
      dev.vm.provision ".stagingrc", type: "file", source: ".stagingrc", destination: "~/.deploymentrc"
    end
  end

  config.vm.define "prod", autostart: false do |prod|
    prod.vm.network "private_network", ip: "172.28.128.11"
    prod.vm.hostname = "share-space-prod"
    if (File.file?(".prodrc"))
      prod.vm.provision ".prodrc", type: "file", source: ".prodrc", destination: "~/.deploymentrc"
    end
  end

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "site", "/home/vagrant/site",  create: true

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = 4
  end

  config.vm.provision "stack-install", type: "shell", privileged: false,               path: "run-env", args: "stack-install"

  # Do not run any of these on up, only with vagrant provision,
  # since the deploymentrc is loaded last on up
  config.vm.provision "stack-build",   type: "shell", privileged: false, run: "never", path: "run-env", args: "stack-build"
  config.vm.provision "stack-up",      type: "shell", privileged: false, run: "never", path: "run-env", args: "stack-up"
  config.vm.provision "stack-down",    type: "shell", privileged: false, run: "never", path: "run-env", args: "stack-down"
  config.vm.provision "stack-status",  type: "shell", privileged: false, run: "never", path: "run-env", args: "stack-status"
end
