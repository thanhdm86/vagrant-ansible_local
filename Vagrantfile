
N = 2

Vagrant.configure("2") do |config|
    config.ssh.insert_key = true
    config.vm.provision "shell", path: "script/base.sh"
    config.vm.provider "virtualbox" do |v|
        v.memory = 3000
        v.cpus = 3
    end

    (1..N).each do |i|
        config.vm.define "node#{i}" do |node|
            node.vm.box = "generic/ubuntu2004"
            node.vm.network "public_network", ip: "192.168.2.#{i + 220}"
            node.vm.hostname = "node#{i}"
           # node.vm.provision "ansible" do |ansible|
           #     ansible.playbook = "kubernetes-setup/node-playbook.yml"
           #     ansible.extra_vars = {
           #         node_ip: "192.168.2.#{i + 10}",
           #     }
            #end 
            node.vm.provision "shell", path: "script/install-k8s.sh"
            node.vm.synced_folder "data", "/mnt/data/"
        end
    end
    config.vm.define "git" do |git|
        git.vm.box = "generic/ubuntu2004"
        git.vm.network "public_network", ip: "192.168.2.200"
        git.vm.hostname = "git"
        git.vm.synced_folder "data", "/mnt/data/"
        end  
    config.vm.define "jenkins" do |jenkins|
        jenkins.vm.box = "generic/ubuntu2004"
        jenkins.vm.network "public_network", ip: "192.168.2.201"
        jenkins.vm.hostname = "jenkins"
        jenkins.vm.synced_folder "data", "/mnt/data/"
        end 
    config.vm.define "docker" do |docker|
        docker.vm.box = "generic/ubuntu2004"
        docker.vm.network "public_network", ip: "192.168.2.202"
        docker.vm.hostname = "docker"
        docker.vm.synced_folder "data", "/mnt/data/"
        end
    config.vm.define "sonar" do |sonar|
        sonar.vm.box = "generic/ubuntu2004"
        sonar.vm.network "public_network", ip: "192.168.2.203"
        sonar.vm.hostname = "sonar"
        sonar.vm.synced_folder "data", "/mnt/data/"
        end
    end 

    

