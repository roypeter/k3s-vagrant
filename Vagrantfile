# -*- mode: ruby -*-
# vi: set ft=ruby :

box = "ubuntu/focal64"

Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
    bash get_helm.sh
  SHELL

  config.vm.define 'node-01' do |node|
    node.vm.box = box
    node.vm.network "private_network", ip: "10.10.9.10"
    node.vm.hostname = "node-01"

    node.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 2
    end

    node.vm.provision "shell", inline: <<-SHELL
      curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s server \
        --cluster-init \
        --no-deploy traefik \
        --flannel-iface enp0s8
      cat /var/lib/rancher/k3s/server/node-token > /vagrant/node-token
    SHELL
  end

  config.vm.define 'node-02' do |node|
    node.vm.box = box
    node.vm.network "private_network", ip: "10.10.9.11"
    node.vm.hostname = "node-02"

    node.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 2
    end

    node.vm.provision "shell", inline: <<-SHELL
      curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s - server \
        --server https://10.10.9.10:6443 \
        --token-file /vagrant/node-token \
        --no-deploy traefik \
        --flannel-iface enp0s8
    SHELL
  end

  config.vm.define 'node-03' do |node|
    node.vm.box = box
    node.vm.network "private_network", ip: "10.10.9.12"
    node.vm.hostname = "node-03"

    node.vm.provider "virtualbox" do |vb|
      vb.memory = 4096
      vb.cpus = 2
    end

    node.vm.provision "shell", inline: <<-SHELL
      curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s - server \
        --server https://10.10.9.10:6443 \
        --token-file /vagrant/node-token \
        --no-deploy traefik \
        --flannel-iface enp0s8
      export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
      helm repo add nginx-stable https://helm.nginx.com/stable
      helm install nginx-ingress nginx-stable/nginx-ingress \
        --set controller.hostNetwork=true \
        --set controller.setAsDefaultIngress=true
      kubectl apply -f /vagrant/sample-app.yaml
    SHELL
  end
end
