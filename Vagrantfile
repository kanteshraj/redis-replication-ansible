# -*- mode: ruby -*-
# vi: set ft=ruby 

Vagrant.configure(2) do |config|
  config.vm.box_check_update = false
  config.vm.synced_folder '.', '/home/vagrant/sync', disabled: true

  config.vm.define :node1 do |node|
    node.vm.box = "centos/7"
    node.vm.network "private_network", ip: "170.11.11.11"
  end

  config.vm.define :node2 do |node|
    node.vm.box = "centos/7"
    node.vm.network "private_network", ip: "170.11.11.12"
  end

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "512"
  end

  config.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
      echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      SHELL
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"

    ansible.groups = {
      "master" => ["node1"],
      "slave"  => ["node2"]
    }
  end
end
