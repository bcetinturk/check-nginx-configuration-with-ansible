# -*- mode: ruby -*-
# vi: set ft=ruby :

machines = [
  {"box" => "ubuntu/focal64", "private_ip" => "192.168.33.10", "name" => "vm_ubuntu20"},
  {"box" => "ubuntu/bionic64", "private_ip" => "192.168.33.11", "name" => "vm_ubuntu18"},
  {"box" => "generic/centos8", "private_ip" => "192.168.33.12", "name" => "centos8"},
]

Vagrant.configure("2") do |config|

  machines.each do |machine|
    config.vm.define machine["name"] do |vm_config|
      vm_config.vm.box = machine["box"]
      vm_config.vm.network "private_network", ip: machine["private_ip"]
      vm_config.vm.provision "ansible" do |ansible|
        ansible.playbook = "nginx-install.yml"
        ansible.ask_become_pass = true
      end
      vm_config.vm.provider "virtualbox" do |vb, override|
        vb.name = machine["name"]
      end

    end
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
