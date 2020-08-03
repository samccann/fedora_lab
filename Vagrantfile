Vagrant.configure("2") do |config|
  network_devices=[
    {
      :hostname => "vyos1",
      :box => "samdoran/vyos",
      :ip => "192.168.57.101",
      :ssh_port => '2210'
    }
  ]

  network_devices.each do |machine|

    config.vm.define machine[:hostname] do |node|
      node.vm.box = machine[:box]
      node.vm.hostname = machine[:hostname]

      node.vm.network :private_network, ip: machine[:ip]
      node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"

      node.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--memory", 512]
        v.customize ["modifyvm", :id, "--name", machine[:hostname]]
      end
    end
  end
end
