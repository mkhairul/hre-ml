# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/focal64"

  config.vm.box_check_update = true
  config.vbguest.auto_update = false
  config.vm.hostname = "hredev"
  config.vm.define "hredev"
  
  config.vm.network :forwarded_port, guest: 80, host: 8000
  config.vm.network :forwarded_port, guest: 3306, host: 3306
  config.vm.network :forwarded_port, guest: 9527, host: 9527
  
  config.vm.provider :virtualbox do |v|
	v.name = "hredev"
	v.customize ["modifyvm", :id, "--ioapic", "on"]
    v.customize ["modifyvm", :id, "--memory", "4096"]
    v.customize ["modifyvm", :id, "--vram", "32"]
	v.customize ["modifyvm", :id, "--cpus", "4"]
  end
  
  config.vm.synced_folder "../work", "/var/www"

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
	sudo add-apt-repository ppa:deadsnakes/ppa
	sudo apt-get update
	sudo apt install python3-pip -y
	sudo apt install mysql-server
	sudo apt-get install libmysqlclient-dev
  #  pip3 install -r requirements.txt
  #  python3 manage.py migrate
  #  apt-get install -y apache2
  SHELL
end
