# -*- mode: ruby -*-
# vi: set ft=ruby :

boxes = [
  { :name => :'log-server',:ip => '192.168.2.120',:ssh_port => 2212,:cpus => 1, :mem => 1024 },
  { :name => :'log-client',:ip => '192.168.2.110',:ssh_port => 2211,:cpus => 1, :mem => 1024 },
  ]

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  boxes.each do |opts|
    config.vm.define opts[:name] do |config|
      config.vm.box       = "chef/centos-6.5"
      config.vm.network  "private_network", ip: opts[:ip]
      config.vm.network  "forwarded_port", guest: 22, host: opts[:ssh_port]
      config.vm.hostname = "%s.vagrant" % opts[:name].to_s
      config.ssh.forward_agent = true
      config.vm.provider "virtualbox" do |vb|
        # Use VBoxManage to customize the VM
        vb.customize ["modifyvm", :id, "--cpus", opts[:cpus] ] if opts[:cpus]
        vb.customize ["modifyvm", :id, "--memory", opts[:mem] ] if opts[:mem]
        vb.customize ["modifyvm", :id, "--ioapic", "on"]
      end
      config.vm.provision "ansible" do |ansible|
        ansible.sudo=true
        ansible.groups = {
          "logclient" => ["log-client"],
          "logserver" => ["log-server"],
          "logging:children" => ["logclient", "logserver"]
        }
        ansible.playbook = "provisioning/site.yml"
      end
    end
  end
end
