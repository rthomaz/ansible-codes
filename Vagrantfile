# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  config.vm.box = "debian/stretch64"
  config.vm.hostname = "deb-01"  
  config.vm.network :public_network, :dev => "br0", :mode => "bridge", :type => "bridge", ip: "192.168.1.185", :netmask => "255.255.255.0"
  config.vm.synced_folder '.', '/vagrant', disabled: true
  
  config.ssh.insert_key = false
    
  config.vm.provider :libvirt do |provider|
    provider.memory = 2048
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
  SHELL

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = ""
#   ansible.verbose = "v"
#   ansible.verbose = "vvvv"
    ansible.playbook = "site.yml"
    ansible.inventory_path = "hosts"
    ansible.limit = "192.168.1.185"
  end
  
end