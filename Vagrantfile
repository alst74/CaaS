Controllers=1
Workers=2

(1..Controllers).each do |controller_id|
  Vagrant.configure("2") do |config|
    config.vm.define "controller#{controller_id}" do |machine|
      config.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbook.yml"
      end
      machine.vm.hostname = "controller#{controller_id}"
      machine.vm.network "private_network", ip: "192.168.11.#{20+controller_id}"
      machine.vm.box = "centos/7"
      machine.vm.provider :virtualbox do |vb|
        vb.customize [
          "modifyvm", :id,
          "--cpuexecutioncap", "75",
          "--memory", "5120",
          "--cpus", "2",
        ]
      end
    end
  end
end
(1..Workers).each do |workers_id|
  Vagrant.configure("2") do |config|
    config.vm.define "worker#{workers_id}" do |machine|
      config.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbook.yml"
      end
      machine.vm.hostname = "worker#{workers_id}"
      machine.vm.network "private_network", ip: "192.168.11.#{50+workers_id}"
      machine.vm.box = "centos/7"
      machine.vm.provider :virtualbox do |vb|
        vb.customize [
          "modifyvm", :id,
          "--cpuexecutioncap", "50",
          "--memory", "5120",
          "--cpus", "2",
        ]
      end
    end
  end
end

#domain = 'docker.lab'
#nodes = [
#  { :hostname => 'docker01', :ip => '192.168.0.20', :sshport => 2022, :box => 'centos/7' },
#  { :hostname => 'docker02', :ip => '192.168.0.21', :sshport => 2023, :box => 'centos/7' },
#  { :hostname => 'docker03', :ip => '192.168.0.22', :sshport => 2024, :box => 'centos/7' }
#]
#
#Vagrant.configure("2") do |config|
#  nodes.each do |node|
#    config.vm.define node[:hostname] do |nodeconfig|
#      nodeconfig.vm.box = node[:box]
#      nodeconfig.vm.hostname = node[:hostname] + ".box"
#      nodeconfig.vm.network :private_network, ip: node[:ip]
#      nodeconfig.vm.network "forwarded_port", guest: 22, host: node[:sshport]
#      memory = node[:ram] ? node[:ram] : 1024;
#      nodeconfig.vm.provider :virtualbox do |vb|
#        vb.customize [
#          "modifyvm", :id,
#          "--cpuexecutioncap", "50",
#          "--memory", memory.to_s,
#        ]
#      end
#    end
#  end
#  config.vm.provision :puppet do |ansible|
#    ansible.playbook = "ansible/playbook.yml"
#  end
#end
