# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.synced_folder "../work", "/work"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end
  config.ssh.forward_agent = true
  config.vm.provision :shell, inline:<<-EOS
    add-apt-repository -y ppa:fkrull/deadsnakes
    apt-get update
    apt-get install -y python3.6 python3.6-dev python3.6-venv build-essential
  EOS
end
