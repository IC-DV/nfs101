# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'open3'
require 'fileutils'

Vagrant.configure("2") do |config|

config.vm.define "server" do |server|
  config.vm.box = 'centos/8.4'
  config.vm.box_url = 'http://cloud.centos.org/centos/8/vagrant/x86_64/images/CentOS-8-Vagrant-8.4.2105-20210603.0.x86_64.vagrant-virtualbox.box'

  server.vm.host_name = "dc.tsty.local"
#  server.vm.network :forwarded_port, guest: 80, host: 8080
#  server.vm.network :forwarded_port, guest: 443, host: 1443
  server.vm.network :private_network, ip: "192.168.56.41"
  server.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end


  server.vm.provision "shell",
    name: "configuration",
    path: "init.sh"
  end


  config.vm.define "client" do |client|
    client.vm.box = 'centos/8.4'
    client.vm.host_name = "client.tsty.local"
    client.vm.network :private_network, ip: "192.168.56.40"
    client.vm.provider :virtualbox do |vb|
      vb.memory = "1024"
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

  config.vm.define "serverv3" do |servernfs|
    servernfs.vm.box = 'centos/7.8'
    servernfs.vm.box_url = 'http://cloud.centos.org/centos/7/vagrant/x86_64/images/CentOS-7-x86_64-Vagrant-2004_01.VirtualBox.box'
    servernfs.vm.host_name = 'nfsv3'
    servernfs.vm.network :private_network, ip: "10.0.0.42"
    servernfs.vm.provider :virtualbox do |vb|
      vb.memory = "1024"
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

end
