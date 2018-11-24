# -*- mode: ruby -*-
# vi: set ft=ruby :

# the "2" is vagrantfile version number
Vagrant.configure("2") do |config|
	
	# Ubuntu Bionic Beaver 18.04
	# Apache 2.4.29
	# PHP 7.2
	# Node.js 8.10.0
	# npm 3.5.2
	# nginx 1.14.0
	# MySQL 5.7.23
	# Composer 1.7.2
	config.vm.box = "houallet/stack"
	
	# this is the ip you will connect to.
	# if you change this, make sure to also change hosts file
	config.vm.network "private_network", ip: "192.168.33.22"

	# synced folder - host computer folder first, then vagrant folder
	config.vm.synced_folder ".", "/var/www/html", 
	create:true, # create directory if not exists
	:owner => 'vagrant',
	:group => 'www-data',
	:mount_options => ['dmode=775','fmode=664']
	
	config.vm.provider "virtualbox" do |vb|
		# Display the VirtualBox GUI when booting the machine
		vb.gui = false
		
		# name shown in virtualbox
		# vb.name = '... Vagrant Box'
		
		# for some reason, without this line, you will get errors with custom boxes:
		# error: RawFile#0 failed to create the raw output file...
		vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
		
		# Customize the amount of memory on the VM:
		vb.memory = "1024"
	end
	
	# sleep will allow the system to finish running unattended updates before running postinstall.
	# this helps prevent the following error:
	# E: Could not get lock /var/lib/dpkg/lock - open (11 Resource temporarily unavailable)
	# E: Unable to lock the administration directory (/var/lib/dpkg/) is another process using it? 
	# it's because Ubuntu and Vagrant are trying to run apt-get update at the same time we are, 
	# 		as the system is booting up.
	# config.vm.provision "shell", inline: "echo 'waiting to avoid dpkg conflicts...' && sleep 30"
	
	# postinstall.sh will run on the machine as sudo when the computer is finished installing.
	# this will only run once. You can manually run it with `vagrant provision`
	# config.vm.provision "shell", path: 'vagrant-postinstall.sh'
end