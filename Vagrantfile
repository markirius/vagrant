# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/buster64"
  config.vm.provision "shell", inline: "curl -fsSL https://get.docker.com | sh"
  config.vm.provider "libvirt" do |v|
    v.memory = "512"
    v.cpus = "1"
  end

  config.vm.define "portainer01" do |portainer01|
    portainer01.vm.network "private_network", ip: "192.168.10.10"
    portainer01.vm.hostname = "portainer01"
    portainer01.vm.synced_folder "/home/nomad/devel/vagrant/portainer/portainer01", "/vagrant", create: true
  end

  config.vm.define "portainer02" do |portainer02|
    portainer02.vm.network "private_network", ip: "192.168.10.11"
    portainer02.vm.hostname = "portainer02"
    portainer02.vm.synced_folder "/home/nomad/devel/vagrant/portainer/portainer02", "/vagrant", create: true
  end

  config.vm.define "portainer03" do |portainer03|
    portainer03.vm.network "private_network", ip: "192.168.10.12"
    portainer03.vm.hostname = "portainer03"
    portainer03.vm.synced_folder "/home/nomad/devel/vagrant/portainer/portainer03", "/vagrant", create: true
  end

end
