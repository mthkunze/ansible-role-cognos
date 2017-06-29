Vagrant.configure(2) do |config|

#  # RedHat 7
#  config.vm.define "redhat", primary: true do |redhat|
#    redhat.vm.box = "redhat7.box"
#    redhat.vm.hostname = "redhat7"
#    redhat.vm.provision "ansible" do |ansible|
#      ansible.playbook = "examples/test_redhat7.yml"
#      ansible.sudo = true
#      ansible.sudo_user = "root"
#      #ansible.tags = "precheck"
#    end
#    redhat.vm.network "forwarded_port", guest: 50000, host: 50000
#    redhat.vm.provider "virtualbox" do |v|
#        v.customize [ "modifyvm", :id, "--cpus", "1" ]
#        v.customize [ "modifyvm", :id, "--memory", "1024" ]
#    end
#  end
  
  # Centos 7
  config.vm.define "centos", primary: true do |centos|
    centos.vm.box = "centos7.box"
    centos.vm.hostname = "centos7"
    centos.vm.provision "ansible" do |ansible|
      ansible.playbook = "examples/test_centos7.yml"
      ansible.sudo = true
      ansible.sudo_user = "root"
      #ansible.tags = "precheck"
    end
    centos.vm.network "forwarded_port", guest: 50000, host: 50000
    centos.vm.provider "virtualbox" do |v|
        v.customize [ "modifyvm", :id, "--cpus", "1" ]
        v.customize [ "modifyvm", :id, "--memory", "1024" ]
    end
  end
  
#  # Ubuntu 16
#  config.vm.define "ubuntu" do |ubuntu|
#    ubuntu.vm.box = "ubuntu/trusty64"
#    ubuntu.vm.hostname = "ubuntu16"
#    ubuntu.vm.network "public_network", ip: "192.168.3.50"
#    ubuntu.vm.provision "ansible" do |ansible|
#      ansible.playbook = "examples/test_ubuntu.yml"
#      ansible.sudo = true
#      ansible.sudo_user = "root"
#    end
#  end

end
