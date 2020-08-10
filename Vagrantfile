# -*- mode: ruby -*-
# vi: set ft=ruby ts=2 sw=2 tw=0 et :
boxes = [
  {
    :name => "haproxy1",
    :box => "bento/centos-7",
    :ip => '10.0.0.200'
  },
  {
    :name => "web1",
    :box => "bento/centos-7",
    :ip => '10.0.0.101'
  },
  {
    :name => "web2",
    :box => "bento/centos-7",
    :ip => '10.0.0.102'
  },
]

Vagrant.configure("2") do |config|
  boxes.each do |box|
    config.vm.synced_folder '.', '/vagrant', disabled: true
    config.vm.boot_timeout = 600
    config.vm.define box[:name] do |vms|
      vms.vm.box = box[:box]
      vms.vm.hostname = "ansible-#{box[:name]}"
      vms.vm.network :private_network, ip: box[:ip]
    end
  end
end
