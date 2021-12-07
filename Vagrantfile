BOX_IMAGE = "ubuntu/focal64"
MASTER_IP = "172.72.72.10"

SERVICE_COUNT = 2

Vagrant.configure("2") do |config|
 config.vm.box = BOX_IMAGE

  config.vm.define "master" do |subconfig|
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "master"
    subconfig.vm.network :private_network, ip: MASTER_IP
    subconfig.vm.provision "shell", inline: 
    "sudo curl -fsSL https://get.docker.com | sh"
  end

  (1..SERVICE_COUNT).each do |service_count|
    config.vm.define "service#{service_count}" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.hostname = "service#{service_count}"
      subconfig.vm.network :private_network, ip: "172.72.72.#{10 + service_count}"
      subconfig.vm.provision "shell", inline: 
      "sudo curl -fsSL https://get.docker.com | sh"
    end
  end

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end
end