# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "jekyll"
  config.vm.define "github-pages" do |base|
  end

  # Throw in our provisioning script
  config.vm.provision "shell", path: "bootstrap.sh", privileged: false, args: 'https://github.com/jehartzog/jehartzog.github.io.git'

  # Map localhost:3000 to port 3000 inside the VM
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "private_network", ip: "192.168.3.33"

  # Create a shared folder between guest and host
  config.vm.synced_folder "www/", "/srv/www", create: true

  config.ssh.forward_agent = true

  # VirtualBox-specific configuration
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", 1024]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

end
