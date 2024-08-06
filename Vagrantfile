# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Use Ubuntu 20.04 (Focal Fossa) as the base box
  config.vm.box = "ubuntu/focal64"

  # Forward port 3000 on the host to port 3000 on the guest
  config.vm.network "forwarded_port", guest: 3000, host: 3000

  # Provisioning configuration for Ansible
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"  # Specify the path to your Ansible playbook
  end

  # (Optional) Uncomment the following lines to enable a private network
  # config.vm.network "private_network", ip: "192.168.33.10"

  # (Optional) Uncomment the following lines to customize the VirtualBox provider settings
  # config.vm.provider "virtualbox" do |vb|
  #   vb.gui = false  # Set to true to display the VirtualBox GUI
  #   vb.memory = "1024"  # Set the memory allocated to the VM
  # end

  # (Optional) Uncomment the following lines to sync an additional folder
  # config.vm.synced_folder "../data", "/vagrant_data"
end
