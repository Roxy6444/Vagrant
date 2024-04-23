# -*- mode: ruby -*-
# vi: set ft=ruby :


current_dir = File.dirname(__FILE__)
Vagrant.configure("2") do |global_config|

cookbook_testers = {
:prometheus1 => {
    :hostname => "prometheus1.example.com",
    :box_name => "ubuntu/trusty64",
    :ipaddress => "10.0.0.118",
    :memory => 6192,
    :cpus => 4,
    :hostport => 2708,
  }
}

  cookbook_testers.each_pair do |name, options|
    global_config.vm.define name do |config|
      config.vm.box = options[:box_name]
      config.vm.host_name = options[:hostname]
      config.vm.network "public_network", ip: options[:ipaddress]
      config.vm.network "public_network", bridge: "bridge0"
      config.vm.network "private_network", ip: options[:ipaddress]
      config.vm.network "forwarded_port", guest: 22, host: options[:hostport]
#      config.vm.synced_folder "/opt/devops/downloads", "/opt/downloads", :owner => "vagrant", :group => "vagrant", :mount_options => ['dmode=775', 'fmode=664']
      config.vm.provider :virtualbox do |vb|
     vb.customize ['modifyvm', :id, '--memory', options[:memory], '--cpus', options[:cpus]]
     vb.name = options[:hostname]
      end
    end
  end
end