# -*- mode: ruby -*-
# vi: set ft=ruby :
#https://github.com/brianc/node-postgres
#http://askubuntu.com/questions/426750/how-can-i-update-my-nodejs-to-the-latest-version

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define :database_app do |masterd|
    masterd.vm.box = "centos_2016"
    masterd.vm.network :private_network, ip: "192.168.56.175"
    masterd.vm.network "public_network", :bridge => "eth1", ip:"192.168.131.175", :auto_config => "false", :netmask => "255.255.255.0"
    masterd.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "4", "--name", "database" ]
    end
      config.vm.provision :chef_solo do |chef1|
      chef1.cookbooks_path = "cookbooks"
      chef1.add_recipe "postgres"
    end
  end
  config.vm.define :nodejs_app do |master|
    master.vm.box = "centos_2016"
    master.vm.network :private_network, ip: "192.168.56.174"
    master.vm.network "public_network", :bridge => "eth1", ip:"192.168.131.174", :auto_config => "false", :netmask => "255.255.255.0"
    master.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "4", "--name", "nodejs_app" ]
    end
      config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = "cookbooks"
      chef.add_recipe "nodejs"
    end
  end
end