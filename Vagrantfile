# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    # Defining machine specific specifications
    # you can change the machine name and box here, if you wish to
    servers=[
        {
            :hostname => "docker-master",
            :box => "ubuntu/bionic64",
            :ip => "172.16.0.5",
        },

        {
            :hostname => "docker-worker1",
            :box => "ubuntu/bionic64",
            :ip => "172.16.0.6",
        },

        {
            :hostname => "docker-worker2",
            :box => "ubuntu/bionic64",
            :ip => "172.16.0.7",
        },
    ]
    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            # Set box
            node.vm.box = machine[:box]
            # Set hostname
            node.vm.hostname = machine[:hostname]
            # Set network
            node.vm.network  :private_network, ip: machine[:ip]
            # install docker and dependecies using provision 
            node.vm.provision "shell", inline: <<-SHELL

                apt-get update
                apt-get remove docker docker-engine docker.io containerd runc
                sudo apt-get -y install \
                    apt-transport-https \
                    ca-certificates \
                    curl \
                    gnupg \
                    lsb-release

                curl -fsSL https://download.docker.com/linux/ubuntu/gpg |  gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
                echo \
                    "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
                    $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null

                sudo apt-get update
                sudo apt-get -y install docker-ce docker-ce-cli containerd.io
                usermod -aG docker vagrant

                SHELL
            # Customize Memory and CPU count as required
            node.vm.provider :virtualbox do |vb|
                vb.customize ["modifyvm", :id, "--memory", "1024"]
                vb.customize ["modifyvm", :id, "--cpus", "2"]
                
            end
        end
    end
end