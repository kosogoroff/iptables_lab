BOX_NAME = ENV['VAGRANT_BOX'] || 'bento/ubuntu-22.04'

MACHINES = {
  :inetRouter => {
        :box_name => BOX_NAME,
        :vm_name => "inetRouter",
        #:public => {:ip => "10.10.10.1", :adapter => 1},
        :net => [   
                    #ip, adpter, netmask, virtualbox__intnet
                    ["192.168.255.1", 2, "255.255.255.252",  "router-net"], 
                    ["192.168.50.10", 8, "255.255.255.0"],
                ]
  },

  :inetRouter2 => {
        :box_name => BOX_NAME,
        :vm_name => "inetRouter2",
        #:public => {:ip => "10.10.10.1", :adapter => 1},
        :net => [
                    #ip, adpter, netmask, virtualbox__intnet
                    ["192.168.255.21", 2, "255.255.255.252",  "router2-net"],
                    ["192.168.50.20", 8, "255.255.255.0"],
                ],
        :fwd => [
          [22, 2332],
          [8080, 8082],
        ],
  },

  :centralRouter => {
        :box_name => BOX_NAME,
        :vm_name => "centralRouter",
        :net => [
                   ["192.168.255.2",  2, "255.255.255.252",  "router-net"],
                   ["192.168.255.22",  3, "255.255.255.252",  "router2-net"],
                   ["192.168.0.1",    4, "255.255.255.240",  "dir-net"],
                   ["192.168.0.33",   5, "255.255.255.240",  "hw-net"],
                   ["192.168.0.65",   6, "255.255.255.192",  "mgt-net"],
                   ["192.168.255.5",  7, "255.255.255.252",  "office2-central"],
                   ["192.168.50.11",  8, "255.255.255.0"],
                ]
  },

  :centralServer => {
        :box_name => BOX_NAME,
        :vm_name => "centralServer",
        :net => [
                   ["192.168.0.2",    2, "255.255.255.240",  "dir-net"],
                   ["192.168.50.12",  8, "255.255.255.0"],
                ]
  }
}

Vagrant.configure("2") do |config|
  MACHINES.each do |boxname, boxconfig|
    config.vm.define boxname do |box|
      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxconfig[:vm_name]
      
      box.vm.provider "virtualbox" do |v|
        v.memory = 768
        v.cpus = 1
       end

      boxconfig[:net].each do |ipconf|
        box.vm.network("private_network", ip: ipconf[0], adapter: ipconf[1], netmask: ipconf[2], virtualbox__intnet: ipconf[3])
      end

      if boxconfig[:fwd]
        boxconfig[:fwd].each do |guest_port, host_port|
          box.vm.network "forwarded_port", guest: guest_port, host: host_port,
            host_ip: "127.0.0.1", auto_correct: true
        end
      end

      if boxconfig.key?(:public)
        box.vm.network "public_network", boxconfig[:public]
      end

      box.vm.provision "shell", inline: <<-SHELL
        mkdir -p ~root/.ssh
        cp ~vagrant/.ssh/auth* ~root/.ssh
      SHELL
    end
  end
end
