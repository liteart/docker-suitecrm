#
# THIS FILE MUST NOT BE EDITED OUTSIDE OF THE VAGRANT_BASE PROJECT IN BITBUCKET!
# PLEASE INTEGRATE ANY CHANGES INSIDE THIS PROJECT AND SYNCHRONIZE THE CHANGES TO ALL OTHER PROJECTS
# shu/2016-10-03
#
# A dummy plugin for Barge to set hostname and network correctly at the very first `vagrant up`
module VagrantPlugins
  module GuestLinux
    class Plugin < Vagrant.plugin("2")
      guest_capability("linux", "change_host_name") { Cap::ChangeHostName }
      guest_capability("linux", "configure_networks") { Cap::ConfigureNetworks }
    end
  end
end

Vagrant.configure(2) do |config|
  config.vm.hostname = 'suitecrmbox' ### <<--- SET THIS HOSTNAME IN RELATION TO YOUR PROJECT ###
  config.vm.define "barge"
  config.vm.box = "ailispaw/barge"
  config.vm.synced_folder ".", "/vagrant"
  config.vm.network "private_network", type: "dhcp"
  config.hostmanager.enabled = false
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true
  cached_addresses = {}
  config.hostmanager.ip_resolver = proc do |vm, resolving_vm|
    if cached_addresses[vm.name].nil?
      if hostname = (vm.ssh_info && vm.ssh_info[:host])
        vm.communicate.execute("/sbin/ifconfig eth1 | grep 'inet addr' | tail -n 1 | egrep -o '[0-9\.]+' | head -n 1 2>&1") do |type, contents|
          cached_addresses[vm.name] = contents.split("\n").first[/(\d+\.\d+\.\d+\.\d+)/, 1]
        end
      end
    end
    cached_addresses[vm.name]
  end
  config.vm.provision :hostmanager
end
