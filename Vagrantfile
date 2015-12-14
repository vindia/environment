# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
API_VERSION = 2

Vagrant.configure(API_VERSION) do |config|
  config.vm.box = 'ubuntu/wily64'
  config.vm.hostname = 'vindia-dev'
  config.vm.network 'private_network', ip: '192.168.47.83'
  config.ssh.forward_agent = true
  config.vm.provision :shell, path: 'provision'
  config.vm.synced_folder ".", "/vagrant", type: "rsync"
  config.vm.synced_folder "~/code", "/vindia", type: "nfs"

  config.vm.provider "virtualbox" do |v|
    host = RbConfig::CONFIG['host_os']

    # Give VM 1/4 system memory & access to all cpu cores on the host
    cpus = `sysctl -n hw.ncpu`.to_i
    # sysctl returns Bytes and we need to convert to MB
    mem = `sysctl -n hw.memsize`.to_i / 1024 / 1024 / 4

    v.customize ["modifyvm", :id, "--memory", mem]
    v.customize ["modifyvm", :id, "--cpus", cpus]
  end
end
