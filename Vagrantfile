# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/bionic64"

  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |vb|
     vb.gui = false
     vb.memory = "2048"
   end


  N = 4
  (1..N).each do |machine_id|
    config.vm.define "node#{machine_id}" do |machine|
      machine.vm.hostname = "machine#{machine_id}"
      machine.vm.network "private_network", ip: "172.17.177.#{20+machine_id}"
      machine.vm.network "forwarded_port", guest: 80, host: "404#{machine_id}"

      if machine_id == N
        machine.vm.provision :ansible do |ansible|
          ansible.playbook       = "ansible/play-with-ansible.yml"
          ansible.verbose        = true
          ansible.limit          = "all" # or only "nodes" group, etc.
          ansible.inventory_path = "ansible/inventory"
        end
      end

    end
  end

end



