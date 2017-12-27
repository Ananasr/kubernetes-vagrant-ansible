nodes = [
  { :hostname => 'master',  :ip => '172.16.66.2', :ram => 2048 },
  { :hostname => 'node1',  :ip => '172.16.66.3', :ram => 1024 },
  { :hostname => 'node2',  :ip => '172.16.66.4', :ram => 1024 },
  { :hostname => 'node3',  :ip => '172.16.66.5', :ram => 1024 }
]

Vagrant.configure("2") do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      nodeconfig.vm.box = "bento/ubuntu-16.04";
      nodeconfig.vm.hostname = node[:hostname] + ".box"
      nodeconfig.vm.network :private_network, ip: node[:ip]
      memory = node[:ram] ? node[:ram] : 256;
      nodeconfig.vm.provider :libvirt do |libvirt|
        libvirt.memory = memory.to_s
        libvirt.cpus = 1
      end
    end
  end

  config.vm.provision "shell", inline: <<-SHELL
    swapoff -a
  SHELL
end
