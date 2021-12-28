
Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 1024
        v.cpus = 2
    end

    Imgs= {
        10 => "bento/ubuntu-20.04",     # YES
        12 => "ubuntu/bionic64",        # (18.04) NO : unsupported compose version
        11 => "ubuntu/trusty64",        # (16.04) NO : vagrant cant connect
    }
      
    Imgs.each do |i, v|
        config.vm.define "vm#{i}" do |master|
            master.vm.box = "#{v}"
            master.vm.network "private_network", ip: "10.0.1.#{i}"
            master.vm.hostname = "vm#{i}"
            master.vm.provision "ansible" do |ansible|
                ansible.playbook = "main.yaml"
            end
        end
    end
end