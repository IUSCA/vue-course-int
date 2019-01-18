# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version '>= 2.0.3'
Vagrant.configure('2') do |config|
	config.vm.network :private_network, type: 'dhcp'
	config.vm.network :forwarded_port, guest: 8080, host: 8080
	config.vm.network :forwarded_port, guest: 5000, host: 5000
	config.vm.define 'vue-cli' do |guest|
		guest.vm.box = 'bento/centos-7.5'
		guest.vm.hostname = 'vue-cli.vagrant.test'
		guest.vm.provider :virtualbox do |vb|
			vb.name = 'vue-cli'
			vb.cpus = '2'
			vb.memory = '2048'
			vb.customize [ 'modifyvm', :id, '--vram', '33' ]
		end
		guest.vm.provision 'ansible' do |ansible|
			ansible.verbose = 'v'
			ansible.compatibility_mode = '2.0'
			ansible.playbook = 'playbooks/vue-cli.yml'
			ansible.become = true
		end
	end
end
