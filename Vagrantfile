Vagrant.configure("2") do |config|
  config.vm.define "elastic-stack" do |elastic|
    elastic.vm.box = "centos/7"
    elastic.vm.network "private_network", ip: "192.168.99.5"
    elastic.vm.hostname = "elastic-stack"

    elastic.vm.provider "virtualbox" do |vm|
      vm.name = "elastic-stack"
      vm.memory = "2048"
      vm.cpus = 2
    end
  end
end
