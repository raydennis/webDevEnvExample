# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  # web VM
  config.vm.define "web" do |web|
    web.vm.box = "centos/7"
    web.vm.network :private_network, ip: "192.168.56.101"
    web.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "web"]
    end
    web.vm.provision "ansible" do |ansible|
      ansible.playbook = "/Users/raydennis/Documents/gitHub/ansible/Playbooks/role-repo.yml"
    end
  end

  # app VM
  config.vm.define "app" do |app|
    app.vm.box = "centos/7"
    app.vm.network :private_network, ip: "192.168.56.102"
    app.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "db"]
    end
    app.vm.provision "ansible" do |ansible|
      ansible.playbook = "/Users/raydennis/Documents/gitHub/ansible/Playbooks/role-repo.yml"
    end
  end

  # development environment vm
  config.vm.define "stdDevEnv" do |stdDevEnv|
    stdDevEnv.vm.box = "unmit/stdDevEnvUbuntu"
    stdDevEnv.vm.network :private_network, ip: "192.168.56.103"
    stdDevEnv.vm.provider :virtualbox do |v|
      v.gui = true
      v.customize ["modifyvm", :id, "--name", "stdDevEnv"]
      v.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
      # Enable copy and paste from the VM to the host and back again
      v.customize [ "modifyvm", :id, "--clipboard", "bidirectional" ]
      # Enable drag and drop from the VM to the host and back again
      v.customize [ "modifyvm", :id, "--draganddrop", "bidirectional" ] 
      # Customize the amount of memory on the VM:
      v.memory = "2048"
    end
    stdDevEnv.vm.provision "ansible" do |ansible|
      ansible.playbook = "/Users/raydennis/Documents/gitHub/ansible/Playbooks/role-repo.yml"
    end
  end

end
