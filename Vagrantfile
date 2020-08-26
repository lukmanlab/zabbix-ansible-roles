IMAGE_NAME = "centos/8"
Z = 1
M = 1

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
      
    (1..Z).each do |i|
        config.vm.define "zabbix-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.99.#{i + 20}"
            node.vm.network "public_network", bridge: "wlp2s0", auto_config: false
            node.vm.provision "shell",
                run: "always",
                inline: "yum install -y net-tools && sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config && reboot"
            node.vm.hostname = "zabbix-#{i}"
            node.vm.provider "virtualbox" do |v|
                v.memory = 2048
                v.cpus = 2
            end
        end
    end
  
    (1..M).each do |i|
        config.vm.define "mysql-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.99.#{i + 30}"
            node.vm.hostname = "mysql-#{i}"
            node.vm.provider "virtualbox" do |v|
                v.memory = 1024
                v.cpus = 1
            end
        end
    end
end