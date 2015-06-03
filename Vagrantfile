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
    freebsd101.vm.network "forwarded_port", guest: 22, host: 2230
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.extra_vars = { ansible_ssh_user: 'vagrant',
                           ansible_python_interpreter: "/usr/bin/env python2"}
  end
end
