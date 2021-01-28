Vagrant.configure("2") do |config|
  config.vm.define "elastic-master" do |master|
    master.vm.box = "generic/ubuntu2004"
    master.vm.network "private_network", ip: "172.16.2.10"
    master.vm.hostname = "elastic-master-1"

    master.vm.provider "virtualbox" do |vm|
      vm.name = "elastic-master-1"
      vm.memory = 4096
      vm.cpus = 2
    end
  end
  (1..2).each do |i|
    config.vm.define "elastic-data-#{i}" do |data|
      data.vm.box = "generic/ubuntu2004"
      data.vm.hostname = "elastic-data-#{i}"
      data.vm.network "private_network", ip: "172.16.2.1#{i}"
      data.vm.provider "virtualbox" do |vb|
        vb.name = "elastic-data-#{i}"
        vb.memory = 4096
        vb.cpus = 2
      end
    end
  end
end
