Vagrant.configure("2") do |config|
    config.vm.box = "centos7"
    config.vm.provider :hyperv do |v|
    v.memory = 2048
    v.cpus = 2
    end
    # Define two VMs with static private IP addresses.
    boxes = [
    { :name => "client",
    :ip => "192.168.9.10",
    },
    { :name => "backup",
    :ip => "192.168.9.15",
    :disks => {
		:sata1 => {
			:dfile => './sata1.vdi',
			:size => 2048,
			:port => 1
        }
    }}
    ]
    # Provision each of the VMs.
    boxes.each do |opts|
    config.vm.define opts[:name] do |config|
    config.vm.hostname = opts[:name]
    config.vm.network "private_network", ip: opts[:ip]
    end
    end
    end