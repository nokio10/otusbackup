Vagrant.configure("2") do |config|
    #config.vm.box = "centos7"
    #config.vm.provider :virtualbox do |v|
    #v.memory = 2048
    #v.cpus = 2
    # Define two VMs with static private IP addresses.
    boxes = [
    { :name => "client",
    :ip => "192.168.56.10",
    },
    { :name => "backup",
    :ip => "192.168.56.15",
    :dfile => './sata1.vdi',
    }
    ]
    # Provision each of the VMs.
    boxes.each do |opts|
    config.vm.define opts[:name] do |config|
    config.vm.hostname = opts[:name]
    config.vm.network "private_network", ip: opts[:ip]
    config.vm.box = "centos7"
    config.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", "2048"]
      if opts[:name] == "backup"
      v.customize ['createhd', '--filename', './sata1.vdi', '--size', 2 * 1024]
      v.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', './sata1.vdi']
      end
   end   
   if opts[:name] == boxes.last[:name]
    config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/main.yaml"
    ansible.become = "true"
    ansible.host_key_checking = "false"
    ansible.limit = "all"
    end
    end
    end
    end
    end

