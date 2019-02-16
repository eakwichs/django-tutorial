# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/bionic64"

  # Create a forwarded port mapping which allows access to a specific port
  config.vm.network "forwarded_port", host_ip: "127.0.0.1", guest: 8080, host: 8080
  config.vm.network "forwarded_port", host_ip: "127.0.0.1", guest: 3306, host: 3306

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    # Update and upgrade the server packages.
    sudo apt-get update
    sudo apt-get -y upgrade

    # Set Ubuntu Language
    sudo locale-gen en_US.UTF-8

    # Install Python 3
    sudo apt-get -y install software-properties-common
    sudo add-apt-repository -y ppa:deadsnakes/ppa
    sudo apt-get update
    sudo apt-get -y install python3.7

    # Install pip, setuptools, and wheel
    cd /tmp && curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
    python3.7 get-pip.py --user

    # Install virtualenv
    pip install virtualenv
  SHELL
end
