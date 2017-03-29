# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox"
  config.vm.provider "vmware_fusion"
  config.vm.box = "redesign/centos7"
  config.vm.box_check_update = true
  config.ssh.forward_agent = true
  config.ssh.insert_key = false

  # Timeouts
  config.vm.boot_timeout = 900
  config.vm.graceful_halt_timeout=100

  config.vm.define :data1, autostart: false do |data1_config|
    data1_config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true
    data1_config.vm.network "private_network", ip: "192.168.22.10", :netmask => "255.255.255.0",  auto_config: true
    #data1_config.vm.network "forwarded_port", id: 'psql', guest: 5432, host: 15432, auto_correct: false
    data1_config.vm.hostname = "master"
    data1_config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512", "--natnet1", "172.16.1/24"]
      vb.gui = false
      vb.name = "master"
    end
  end

  config.vm.define :data2, autostart: false do |data2_config|
    data2_config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true
    data2_config.vm.network "private_network", ip: "192.168.22.11", :netmask => "255.255.255.0",  auto_config: true
    data2_config.vm.network "forwarded_port", id: 'psql', guest: 5432, host: 15432, auto_correct: false
    data2_config.vm.hostname = "slave"
    data2_config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512", "--natnet1", "172.16.1/24"]
      vb.gui = false
      vb.name = "slave"
    end
  end

  config.vm.define :target, autostart: true do |target_config|
    target_config.vm.network "private_network", ip: "192.168.22.12", :netmask => "255.255.255.0",  auto_config: true
    target_config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024", "--natnet1", "172.16.1/24"]
      vb.gui = false
      vb.name = "target"
    end
  end

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
    app2_config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true
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
