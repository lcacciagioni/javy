$script = <<SCRIPT
setenforce 0
export DEBIAN_FRONTEND=noninteractive
ansible --version || dnf -y install ansible python-dnf
cd /vagrant
export PYTHONUNBUFFERED=1
ansible-playbook -i local_inventory -b -c local provision.yml
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "fedora/23-cloud-base"

  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.provision "shell", inline: $script
end
