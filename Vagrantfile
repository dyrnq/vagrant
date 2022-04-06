# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

NODE_IP_NW   = "192.168.19."

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bullseye64"
  #config.vm.box = "ubuntu/focal64"
  config.vm.box_check_update = true
  config.ssh.insert_key = false
  config.ssh.private_key_path = "insecure_private_key"
  # config.ssh.username = "vagrant"
  # config.ssh.password = "vagrant"

  

  # config.hostmanager.enabled = true
  # config.hostmanager.manage_guest = true

  (1..6).each do |i|
    hostname= "vm#{i}"
    config.vm.define(hostname) do |node|
      node.vm.hostname = hostname
      node.vm.network :private_network, ip: NODE_IP_NW + "#{i + 10}"
      node.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--vram", "32"]
        vb.customize ["modifyvm", :id, "--ioapic", "on"]
        vb.customize ["modifyvm", :id, "--cpus", "2"]
        vb.customize ["modifyvm", :id, "--memory", "2048"]
      end
      node.vm.provision "shell", inline: <<-SHELL
        echo "root:vagrant" | sudo chpasswd
        timedatectl set-timezone "Asia/Shanghai"
      SHELL
    end
  end

end