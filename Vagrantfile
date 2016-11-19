# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "centos/7"

    config.vm.synced_folder ".", "/vagrant", disabled: true
    # config.vm.synced_folder "./shared", "/home/vagrant/shared", type: "virtualbox"

    config.vm.hostname = "vagrant.dev"
    config.vm.network "private_network", ip: "10.10.10.42"

    # config.landrush.enabled = true
    # config.landrush.tld = 'dev'

    config.vm.provision :shell, path: "provision"
end
