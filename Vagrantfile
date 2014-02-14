# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  config.vm.define :ruby0 do |cfg|
    cfg.vm.network :private_network, ip: "192.168.33.10"
    cfg.vm.provider :virtualbox do |v|
      v.name = "ruby0"
      v.customize ["modifyvm", :id, "--memory", 384]
    end
  end

  config.vm.define :ruby1 do |cfg|
    cfg.vm.network :private_network, ip: "192.168.33.11"
    cfg.vm.provider :virtualbox do |v|
      v.name = "ruby1"
      v.customize ["modifyvm", :id, "--memory", 384]
    end


    config.vm.provision "ansible" do |ansible|
      # Required to "warm up" the network
      # God knows why this is required
      (10..11).each do |ip|
        system("ping -c2 192.168.33.#{ip} > /dev/null")
      end
      ansible.playbook = "setup-vagrant.yml"
      ansible.host_key_checking = false
      ansible.inventory_path = "hosts"
    end
  end

end
