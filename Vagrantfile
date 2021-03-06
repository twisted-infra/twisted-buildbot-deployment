# -*- mode: ruby -*-

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.network :forwarded_port, guest: 22, host: 2222, id: "ssh", disabled: true

  config.vm.provider "virtualbox" do |v|
      v.cpus = 1
      v.memory = 2048
  end

  config.vm.define "freebsd-10.1" do |freebsd101|
    freebsd101.vm.box = "http://iris.hosting.lv/freebsd-10.1-amd64.box"
    freebsd101.vm.network "forwarded_port", guest: 22, host: 2430
  end

  config.vm.define "debian-7" do |box|
    box.vm.box = "chef/debian-7.8"
    box.vm.network "forwarded_port", guest: 22, host: 2431
  end

  config.vm.define "debian-8" do |box|
    box.vm.box = "https://github.com/holms/vagrant-jessie-box/releases/download/Jessie-v0.1/Debian-jessie-amd64-netboot.box"
    box.vm.network "forwarded_port", guest: 22, host: 2432
  end

  config.vm.define "fedora-22" do |box|
    box.vm.box = "boxcutter/fedora22"
    box.vm.network "forwarded_port", guest: 22, host: 2433
  end

  config.vm.define "ubuntu-15.04" do |box|
    box.vm.box = "ubuntu/vivid64"
    box.vm.network "forwarded_port", guest: 22, host: 2434
  end


  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.extra_vars = { ansible_ssh_user: 'vagrant',
                           ansible_python_interpreter: "/usr/bin/env python2"}
  end
end
