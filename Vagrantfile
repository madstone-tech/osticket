# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.


Vagrant.configure("2") do |config|
    config.vm.box = "gbailey/amzn2"
    config.ssh.insert_key = true
  
    config.vm.define "db", primary: true do |db|
      db.vm.provider "virtualbox" do |v|
          v.customize ["modifyvm", :id, "--memory", "2048", "--cpus", "2"]
      end
      db.vm.network :private_network, ip: "192.168.44.11"
      db.vm.hostname = "db"
      db.vm.network :forwarded_port, guest: 3306, host: 3306
      db.vm.network :forwarded_port, guest: 22, host: 2222
        
      config.vm.provision "ansible" do |ansible|
        ansible.inventory_path = "dev"
        ansible.playbook = "db.yml"
        ansible.verbose = "v" 
      end
    end
  
    config.vm.define "web" do |web|
      web.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--memory", "2048", "--cpus", "2"]
      end
      web.vm.network :private_network, ip: "192.168.44.10"
      web.vm.hostname = "web"
      web.vm.network :forwarded_port, guest: 80,   host: 8080
      web.vm.network :forwarded_port, guest: 443,  host: 8843
      web.vm.network :forwarded_port, guest: 22, host: 2200
  
        
      config.vm.provision "ansible" do |ansible|
        ansible.inventory_path = "dev"
        ansible.playbook = "web.yml"
        ansible.verbose = "v" #up to "vvvv" to debug
      end
  
    end
  end