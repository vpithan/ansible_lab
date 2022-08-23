# -*- mode: ruby -*-
# vi: set ft=ruby :

machines = {
  "ansible"   => {"memory" => "1024", "cpu" => "2", "ip" => "30", "image" => "ubuntu/focal64"},
  "machine01" => {"memory" => "512",  "cpu" => "2", "ip" => "31", "image" => "debian/buster64"},
  "machine02" => {"memory" => "512",  "cpu" => "2", "ip" => "32", "image" => "centos/7"},
  "machine03" => {"memory" => "512",  "cpu" => "2", "ip" => "33", "image" => "debian/buster64"}
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}.caiodelgado.example"
      machine.vm.network "private_network", ip: "10.10.10.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        vb.customize ["modifyvm", :id, "--groups", "/mentoria"]
      end
      if "#{name}" == "ansible"
        machine.vm.provision "shell", inline: "apt-get update && apt-get install -y ansible"
      else
        machine.vm.provision "shell", inline: "cat /vagrant/key.pub >> /home/vagrant/.ssh/authorized_keys"
      end
    end
    config.ssh.extra_args = ["-t", "cd /vagrant; bash --login"]
  end
end
