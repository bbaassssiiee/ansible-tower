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

  config.vm.define :data1, autostart: true do |data1_config|
    # disable guest additions
    data1_config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: false
    data1_config.vm.network "private_network", ip: "192.168.22.10", :netmask => "255.255.255.0",  auto_config: true
    #data1_config.vm.network "forwarded_port", id: 'psql', guest: 5432, host: 15432, auto_correct: true
    data1_config.vm.hostname = "master"
    data1_config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512", "--natnet1", "172.16.1/24"]
      vb.gui = false
      vb.name = "master"
    end
  end

  config.vm.define :data2, autostart: false do |data2_config|
    # disable guest additions
    data2_config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: false
    data2_config.vm.network "private_network", ip: "192.168.22.11", :netmask => "255.255.255.0",  auto_config: true
    # data2_config.vm.network "forwarded_port", id: 'psql', guest: 5432, host: 15432, auto_correct: true
    data2_config.vm.hostname = "slave"
    data2_config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512", "--natnet1", "172.16.1/24"]
      vb.gui = false
      vb.name = "slave"
    end
  end

#  config.vm.define :data3, autostart: false do |data3_config|
#    data3_config.vm.network "private_network", ip: "192.168.22.12", :netmask => "255.255.255.0",  auto_config: true
#    data3_config.vm.provider "virtualbox" do |vb|
#      vb.customize ["modifyvm", :id, "--memory", "1024", "--natnet1", "172.16.1/24"]
#      vb.gui = false
#      vb.name = "data3"
#    end
#  end

  config.vm.define :app1,  primary: true do |app1_config|
    app1_config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: false
    app1_config.vm.network "private_network", ip: "192.168.22.13", :netmask => "255.255.255.0",  auto_config: true
    app1_config.vm.hostname = "tower"
    app1_config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "4096", "--natnet1", "172.16.1/24"]
      vb.customize ["modifyvm", :id, "--ioapic", "on"  ]
      vb.name = "tower"
      vb.gui = false
    end
  end

  config.vm.define :app2,  autostart: false do |app2_config|
  # disable guest additions
    app2_config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: false
    app2_config.vm.network "private_network", ip: "192.168.22.14", :netmask => "255.255.255.0",  auto_config: true
    app2_config.vm.hostname = "standby"
    app2_config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "4096", "--natnet1", "172.16.1/24"]
      vb.customize ["modifyvm", :id, "--ioapic", "on"  ]
      vb.name = "standby"
      vb.gui = false
    end
  end

end


