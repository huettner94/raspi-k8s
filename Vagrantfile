IMAGE_NAME = "generic/ubuntu1604"
N = 3

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
    config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"

    config.vm.provider "libvirt" do |libvirt|
        libvirt.memory = 2048
        libvirt.cpus = 2
        libvirt.storage :file, :size => '20G'
    end


    (1..N).each do |i|
        config.vm.define "raspi-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.50.#{i + 10}", :libvirt__guest_ipv6 => "no"
            node.vm.hostname = "node-#{i}"
        end
    end
end
