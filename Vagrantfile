# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/bionic64"

  # CockroachDB
  (1..3).each do |i|
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    config.vm.define "cockroachdb0#{i}" do |server|
      server.vm.hostname = "cockroachdb0#{i}"
      server.vm.network "private_network", ip: "10.0.5.3#{i}"
    end
  end

  # Provision
  config.vm.provision "shell", path: "provision.sh"
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/id_rsa.pub"
  config.vm.provision "shell", :inline => "cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys", run: "always"

end
