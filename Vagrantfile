# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
	config.vm.provider "virtualbox"
	config.vm.box = "testdc01"
	config.vm.guest = :windows 
	config.vm.communicator = "winrm"
	config.vm.hostname = "DC01"
	config.vm.base_mac = "0800279013FA"
	config.vm.boot_timeout = 600 
	config.vm.graceful_halt_timeout = 600
	config.vm.network :forwarded_port, guest: 3389, host: 3389 
	config.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true
	 
	#	 
	
	config.vm.provision :shell, :path => "https://raw.githubusercontent.com/mikensec/ADGenerator/main/Invoke-ForestDeploy.ps1"
	config.vm.provision :shell, :path => "https://raw.githubusercontent.com/mikensec/ADGenerator/main/ADGenerator.ps1"
    
	
	# Network Settings for guest system
	config.vm.network "private_network", ip: "192.168.3.8",
		virtualbox__intnet: "External"
	config.vm.network "private_network", ip: "192.168.16.7",
		virtualbox__intnet: "Internal"
	config.vm.network "private_network", ip: "10.120.116.75",
		virtualbox__intnet: "Secure"
		
	config.vm.provider "virtualbox" do |v|
		v.gui = true
		v.name = "DC01vagrant"
		v.memory = 2048
		v.cpus = 2
		
		#Set up networks on VirtualBox
		v.customize ["natnetwork", "remove", "--netname", "External"]
		v.customize ["natnetwork", "remove", "--netname", "Internal"]
		v.customize ["natnetwork", "remove", "--netname", "Secure"]
		v.customize ["natnetwork", "add", "--netname", "External", "--network", "192.168.3.0/24", "--enable", "--dhcp", "on"]
		v.customize ["natnetwork", "add", "--netname", "Internal", "--network", "192.168.16.0/24", "--enable", "--dhcp", "on"]
		v.customize ["natnetwork", "add", "--netname", "Secure", "--network", "10.120.116.0/24", "--enable", "--dhcp", "on"]
	end	
	
	
end
