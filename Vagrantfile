# -*- mode: ruby -*-
# vi: set ft=ruby :

box = "ubuntu/focal64"

Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
  SHELL

  config.vm.define 'node-01' do |node|
    node.vm.box = box
    node.vm.network "private_network", ip: "10.10.9.10"
    node.vm.hostname = "node-01"
    node.vm.provision "shell", inline: <<-SHELL
    SHELL
  end
  config.vm.define 'node-02' do |node|
    node.vm.box = box
    node.vm.network "private_network", ip: "10.10.9.11"
    node.vm.hostname = "node-02"
    node.vm.provision "shell", inline: <<-SHELL
    SHELL
  end
  config.vm.define 'node-03' do |node|
    node.vm.box = box
    node.vm.network "private_network", ip: "10.10.9.12"
    node.vm.hostname = "node-03"
    node.vm.provision "shell", inline: <<-SHELL
    SHELL
  end
end
