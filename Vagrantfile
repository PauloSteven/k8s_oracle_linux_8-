Vagrant.configure("2") do |config|
    servers=[
        {
          :hostname => "deployer",
          :box => "generic/rocky8",
          :ip => "10.23.45.2",
          :ssh_port => '2204'
        },
        {
          :hostname => "control",
          :box => "generic/rocky8",
          :ip => "10.23.45.3",
          :ssh_port => '2201'
        },
        {
          :hostname => "node1",
          :box => "generic/rocky8",
          :ip => "10.23.45.4",
          :ssh_port => '2202'
        },
        {
          :hostname => "node2",
          :box => "generic/rocky8",
          :ip => "10.23.45.5",
          :ssh_port => '2205'
        }
      ]

    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
            node.vm.network :private_network, ip: machine[:ip]
            node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
            node.vm.provider :virtualbox do |vb|
                vb.customize ["modifyvm", :id, "--memory", 2048]
                vb.customize ["modifyvm", :id, "--cpus", 2]
            end
        end
    end
end
