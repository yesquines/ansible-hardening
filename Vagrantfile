# -*- mode: ruby -*-
# vi: set ft=ruby :
# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
secmachines = {
  'debian' => {'box' => 'debian/buster64','memory' => '2048', 'cpus' => 1, 'ip' => '172.27.2.2'},
  'centos' => {'box' => 'centos/8','memory' => '2048', 'cpus' => 1, 'ip' => '172.27.2.3'},
}

Vagrant.configure("2") do |config|
  secmachines.each do |name, machines|
    config.vm.define "#{name}" do |server|
      server.vm.hostname = "#{name}.machine.example"
      server.vm.box = "#{machines['box']}"
      server.vm.box_check_update = false
      server.vm.network "private_network", ip: "#{machines['ip']}", dns: "8.8.8.8" 

      server.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--groups", "/AnsibleHardening"]
        vb.memory = "#{machines['memory']}"
        vb.cpus = "#{machines['cpus']}"
        vb.name = "#{name}"
      end

      if "#{name}" == "centos"
        server.vm.provision "shell", inline: "dnf install -q -y python3 > /dev/null"
      else
        server.vm.provision "shell", inline: "DEBIAN_FRONTEND=noninteractive apt-get install -qq -y python3 > /dev/null"
      end

    end
  end
end
