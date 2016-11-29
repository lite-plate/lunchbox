# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    # use latest CentOS 7 box as base
    config.vm.box = "centos/7"


    # disable default synced folder to remove dependency on guest additions
    config.vm.synced_folder ".", "/vagrant", disabled: true


    # set basic network configuration
    config.vm.hostname = "vagrant.dev"
    config.vm.network "private_network", ip: "10.10.10.42"


    # find 1/4 system memory in MB
    host = RbConfig::CONFIG['host_os']
    if host =~ /darwin/
        mem = `sysctl -n hw.memsize`.to_i / 1024
    elsif host =~ /linux/
        mem = `grep 'MemTotal' /proc/meminfo | sed -e 's/MemTotal://' -e 's/ kB//'`.to_i
    elsif host =~ /mswin|mingw|cygwin/
        mem = `wmic computersystem Get TotalPhysicalMemory`.split[1].to_i / 1024
    end
    mem = mem / 1024 / 4


    # virtualbox VM configuration
    config.vm.provider "virtualbox" do |v|
        v.cpus = 2
        v.customize ["modifyvm", :id, "--memory", mem]
    end


    # upload SSH files from guest-ssh to ~/.ssh directory on guest
    config.vm.provision "file", source: "guest-ssh", destination: "/tmp/guest-ssh"


    # upload executable files from guest-bin to guest ~/bin directory
    config.vm.provision "file", source: "guest-bin", destination: "/tmp/guest-bin"


    # install packages and configure box
    config.vm.provision :shell, path: "provision"
end
