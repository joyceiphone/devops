Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.provider "virtualbox" do |vbox|
    vbox.memory = 4096
    vbox.cpus = 2
  end
  config.vm.network "private_network", type: "dhcp"
  config.vm.hostname = "minikube"
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end
  config.vm.network "forwarded_port", guest: 5000, host: 5000, autocorrect: true
end