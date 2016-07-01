# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox"
  config.vm.provider "vmware_fusion"
  config.vm.box = "Opscode centos-6.5"
  config.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_centos-6.5_chef-provisionerless.box"
  config.vm.box_check_update = true
  config.ssh.forward_agent = false
  config.ssh.insert_key = false

  # Timeouts
  config.vm.boot_timeout = 900
  config.vm.graceful_halt_timeout=100

  # If ansible is in your path it will provision from your HOST machine
  # If ansible is not found in the path it will be instaled in the VM and provisioned from there
  config.vm.provision "ansible" do |ansible|
    ansible.inventory_path = "inventory.ini"
    ansible.playbook = "deploy.yml"
#    ansible.raw_arguments = "--ask-vault-pass"
    ansible.verbose = "vv"
    ansible.host_key_checking = "false"
  end

  #config.vm.synced_folder "./", "/vagrant", :nfs => true, :mount_options => ['vers=3','noatime','actimeo=2', 'tcp', 'fsc']

  config.vm.define :data1, autostart: true do |data1_config|
    data1_config.vm.network "private_network", ip: "192.168.22.10", :netmask => "255.255.255.0",  auto_config: true
    data1_config.vm.network "forwarded_port", id: 'psql', guest: 5432, host: 15432, auto_correct: true
		data1_config.vm.network "forwarded_port", id: 'mongo', guest: 27010, host: 27010, auto_correct: true
    data1_config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024", "--natnet1", "172.16.1/24"]
      vb.gui = false
      vb.name = "data1"
    end
  end

  config.vm.define :data2, autostart: true do |data2_config|
    data2_config.vm.network "private_network", ip: "192.168.22.11", :netmask => "255.255.255.0",  auto_config: true
    data2_config.vm.network "forwarded_port", id: 'psql', guest: 5432, host: 25432, auto_correct: true
		data2_config.vm.network "forwarded_port", id: 'mongo', guest: 27020, host: 27020, auto_correct: true
    data2_config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024", "--natnet1", "172.16.1/24"]
      vb.gui = false
      vb.name = "data2"
    end
  end

#  config.vm.define :data3, autostart: true do |data3_config|
#    data3_config.vm.network "private_network", ip: "192.168.22.12", :netmask => "255.255.255.0",  auto_config: true
#		data3_config.vm.network "forwarded_port", id: 'mongo', guest: 27030, host: 27030, auto_correct: true
#    data3_config.vm.provider "virtualbox" do |vb|
#      vb.customize ["modifyvm", :id, "--memory", "1024", "--natnet1", "172.16.1/24"]
#      vb.gui = false
#      vb.name = "data3"
#    end
#  end

  config.vm.define :app1,  primary: true do |app1_config|
    app1_config.vm.network "private_network", ip: "192.168.22.13", :netmask => "255.255.255.0",  auto_config: true
    app1_config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "4096", "--natnet1", "172.16.1/24"]
      vb.customize ["modifyvm", :id, "--ioapic", "on"  ]
      vb.name = "app1"
      vb.gui = false
    end
  end

  config.vm.define :app2,  primary: true do |app2_config|
    app2_config.vm.network "private_network", ip: "192.168.22.14", :netmask => "255.255.255.0",  auto_config: true
    app2_config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "4096", "--natnet1", "172.16.1/24"]
      vb.customize ["modifyvm", :id, "--ioapic", "on"  ]
      vb.name = "app2"
      vb.gui = false
    end
  end

end


