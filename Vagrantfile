# -*- mode: ruby -*-
# vi: set ft=ruby :

API_VERSION = "2"
VM_PROVIDER = "libvirt"
WORKERS = 3
VM_MEMORY = 1024
VM_CPUS = 2

Vagrant.configure(API_VERSION) do |config|

  config.vm.provision "shell", inline: "curl -fsSL https://get.docker.com | sh"
  config.vm.provider VM_PROVIDER do |v|
    v.memory = VM_MEMORY
    v.cpus = VM_CPUS
  end

  (1..WORKERS).each do |i|
    config.vm.define "portainer-#{i}" do |node|
      node.vm.hostname = "portainer-#{i}"
      node.vm.box = "debian/buster64"
      node.vm.network :private_network, ip: "192.168.10.#{10+i}"
      node.vm.synced_folder "./shared", "/vagrant", create: true
      if node.vm.hostname != "portainer-1"
        node.vm.provision "shell", inline: "sleep 60 && cat /vagrant/join | grep '^ ' | sh", privileged: true
      end
      if node.vm.hostname == "portainer-1"
        node.vm.provision "shell", inline: "curl -L https://downloads.portainer.io/ce2-17/portainer-agent-stack.yml -o ~/portainer-agent-stack.yml"
        node.vm.provision "shell", inline: "docker swarm init --advertise-addr 192.168.10.#{10+i} > /vagrant/join", privileged: true
        node.vm.provision "shell", inline: "docker stack deploy -c ~/portainer-agent-stack.yml portainer", privileged: true
      end # if node

    end # config

  end # workers

end 
