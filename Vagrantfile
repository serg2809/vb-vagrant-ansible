Vagrant.configure("2") do |config|
  config.vm.box = "bento/fedora-28"
 #config.vm.network "public_network", type: "dhcp"
config.vm.network "private_network", ip: "192.168.33.10"
# change those lines whether you need more RAM or CPUs
config.vm.provider "virtualbox" do |v|
v.name = "fedora-node1"
v.memory = 2048
v.cpus = 1
# tweak to workaround dns issues 
 v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
end

config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook.yml"
#    ansible.install = "true"
#    ansible.install_mode = "default"
#    ansible.verbose = "true"
#    ansible.inventory_path="/vagrant/inventory"
  end
  
end
