# -*- mode: ruby -*-
# vi: set ft=ruby :

machines = [
  {"box" => "ubuntu/focal64", "private_ip" => "192.168.33.10", "name" => "vm_ubuntu20"},
  {"box" => "ubuntu/bionic64", "private_ip" => "192.168.33.11", "name" => "vm_ubuntu18"},
  {"box" => "generic/centos8", "private_ip" => "192.168.33.12", "name" => "vm_centos8"},
]

ssh_public_key_file = "#{Dir.home}/.ssh/id_rsa.pub"

Vagrant.configure("2") do |config|

  # machines.each do |machine|
  #   config.vm.define machine["name"] do |vm_config|
  #     vm_config.vm.box = machine["box"]
  #     vm_config.vm.network "private_network", ip: machine["private_ip"]

  #     vm_config.vm.provision "shell" do |shell|
  #       ssh_public_key = File.readlines(ssh_public_key_file).first.strip
  #       shell.inline = <<-SHELL
  #         echo #{ssh_public_key} >> /home/vagrant/.ssh/authorized_keys
  #       SHELL
  #     end

  #     vm_config.vm.provision "ansible" do |ansible|
  #       ansible.inventory_path = "inventory/hosts"
  #       ansible.playbook = "nginx-install.yml"
  #       ansible.ask_become_pass = true
  #     end

  #     vm_config.vm.provider "virtualbox" do |vb, override|
  #       vb.name = machine["name"]
  #     end

  #   end
  # end

  config.vm.define "vm_ubuntu20_jenkins" do |vm_config|
    vm_config.vm.box = "ubuntu/focal64"
    vm_config.vm.network "private_network", ip: "192.168.33.13"
    
    vm_config.vm.provider "virtualbox" do |vb, override|
      vb.name = "vm_ubuntu20_jenkins"
    end

    vm_config.vm.provision "shell" do |shell|
      ssh_public_key = File.readlines(ssh_public_key_file).first.strip
      shell.inline = <<-SHELL
        echo #{ssh_public_key} >> /home/vagrant/.ssh/authorized_keys
      SHELL
    end

    vm_config.vm.provision "ansible" do |ansible|
      ansible.inventory_path = "inventory/hosts"
      ansible.playbook = "jenkins-install.yml"
      ansible.ask_vault_pass = true
    end

  end

end
