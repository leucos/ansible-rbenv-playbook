# -*- mode: ruby -*-
# vi: set ft=ruby :

hosts = {
  "ruby0" => "192.168.33.10",
  "ruby1" => "192.168.33.11",
}

Vagrant.configure("2") do |config|
  hosts.each do |name, ip|
    config.vm.define name do |machine|
      machine.vm.box = "precise32"
      machine.vm.box_url = "http://files.vagrantup.com/precise32.box"
      machine.vm.hostname = "%s.example.org" % name
      machine.vm.network :private_network, ip: ip
      machine.vm.provider "virtualbox" do |v|
          v.name = name
          v.customize ["modifyvm", :id, "--memory", 512]
      end
      config.vm.provision "ansible" do |ansible|
        ansible.playbook = "setup-vagrant.yml"
        ansible.host_key_checking = false
      end
    end
  end
end
