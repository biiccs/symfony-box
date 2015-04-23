# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANT_API_VERSION = "2"
MACHINE_HOSTNAME = "vm-gofast"

Vagrant.configure(VAGRANT_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.network :private_network, ip: "192.168.2.2"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
   config.vm.synced_folder ".", "/vagrant", disabled: true
   config.vm.synced_folder ".", "/vagrant", type: "nfs", group: nil, owner: nil

  # config.vm.synced_folder ".", "/vagrant", type: "rsync"


  # config.vm.synced_folder ".", "/vagrant", :nfs => { :mount_options => ["dmode=777","fmode=777"] }
  # config.vm.synced_folder ".", "/vagrant", :nfs => true
  # config.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777","fmode=666"]
  # config.vm.synced_folder ".", "/vagrant", id: "application", :mount_options => ["dmode=777","fmode=666"], :nfs => true

    config.vm.provider :virtualbox do |vb|
        vb.gui = false
        vb.customize ["modifyvm", :id, "--name", MACHINE_HOSTNAME]
  #      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--memory", 2048]
  #      vb.customize ["modifyvm", :id, "--cpus", 8]
  #      vb.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "./provision/ansible/site.yml"
        ansible.sudo = true
        ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
    end

    config.vm.define MACHINE_HOSTNAME do |machine|
      machine.vm.hostname = MACHINE_HOSTNAME
    end
end
