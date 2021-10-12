# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
	config.vm.synced_folder ".", "/vagrant", disabled: true
	config.vm.define :router do |router|
		router.vm.box = "debian/bullseye64"
		router.vm.hostname = "router"
		router.vm.network :public_network,
				  :dev => "br0",
				  :mode => "bridge",
                                  :type => "bridge"
		router.vm.network :private_network,
                                  :libvirt__network_name => "red_ej2",
				  :libvirt__dhcp_enabled => false,
                                  :libvirt__forward_mode => "veryisolated",
				  :ip => "10.0.0.1"
	end
	config.vm.define :cliente do |cliente|
		cliente.vm.box = "debian/bullseye64"
		cliente.vm.hostname = "cliente"
		cliente.vm.network :private_network,
                                   :libvirt__network_name => "red_ej2",
				   :libvirt__dhcp_enabled => false,
                                   :libvirt__forward_mode => "veryisolated",
				   :ip => "10.0.0.2"
	end
	config.vm.provision "ansible" do |ansible|
		ansible.playbook="./ansible/site.yaml"
	end
end
