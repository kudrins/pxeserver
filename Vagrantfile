# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
config.vm.synced_folder ".", "/vagrant", disabled: true
config.vm.define "pxeserver" do |server|
# используется локальный образ CentOS 8 Stream
  server.vm.box = 'centos8'
# добавляется диск необходимого размера
  server.vm.disk :disk, size: "30GB", name: "extra_storage1"

  server.vm.host_name = 'pxeserver'
  server.vm.network :private_network, 
                     ip: "10.0.0.20", 
                     virtualbox__intnet: 'pxenet'
  server.vm.network :private_network,
                     ip: "192.168.50.20" 
  server.vm.network "forwarded_port", guest: 80, host: 8081

  server.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

config.vm.provision "shell", inline: <<-SHELL
  sudo sed -i '/PasswordAuthentication no/d' /etc/ssh/sshd_config    
  sudo systemctl restart sshd.service
SHELL
  
end

  config.vm.define "pxeclient" do |pxeclient|
# используется локальный образ CentOS 8 Stream
    pxeclient.vm.box = '/home/sergey/otus/test/package.box'
    pxeclient.vm.host_name = 'pxeclient'
    pxeclient.vm.network :private_network, ip: "10.0.0.21"
    pxeclient.vm.provider :virtualbox do |vb|
      vb.memory = "4096"
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vb.customize [
          'modifyvm', :id,
          '--nic1', 'intnet',
          '--intnet1', 'pxenet',
          '--nic2', 'nat',
          '--boot1', 'net',
          '--boot2', 'none',
          '--boot3', 'none',
          '--boot4', 'none'
        ]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

end
