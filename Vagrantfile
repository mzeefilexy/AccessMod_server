# -*- mode: ruby -*-
# vi: set ft=ruby :
#      ___                                  __  ___            __   ______
#     /   |  _____ _____ ___   _____ _____ /  |/  /____   ____/ /  / ____/
#    / /| | / ___// ___// _ \ / ___// ___// /|_/ // __ \ / __  /  /___ \  
#   / ___ |/ /__ / /__ /  __/(__  )(__  )/ /  / // /_/ // /_/ /  ____/ /  
#  /_/  |_|\___/ \___/ \___//____//____//_/  /_/ \____/ \__,_/  /_____/   
#                                                                         
# Author : Fred Moser <moser.frederic@gmail.com>
# Date : 3 april 2015
# 
# Script to configure virtual box VM using Vagrant.
# Provisioning is done with provision.sh
#

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  #config.vm.box = "https://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-vagrant.box"
  config.vm.box = "gbarbieru/xenial";
 
  # name and basic config of the VM
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
    v.name = "accessmodServer"
  end
  config.vm.provision "shell", path: "provision.sh"
  config.vm.network "forwarded_port", guest: 3838, host: 8080
  config.vm.hostname = "accessmod"
  config.vm.synced_folder ".", "/vagrant", disabled: true
  
  # Additional setup 
  config.vm.provider "virtualbox" do |v|
    # For 3 cards, set type of network hardware to virtualize or software interface to use
    # virtio = not virtualized by virtualbox, but interface expected from guest : 
    v.customize ["modifyvm", :id, "--nictype1", "virtio"]
    v.customize ["modifyvm", :id, "--nictype2", "virtio"]
    v.customize ["modifyvm", :id, "--nictype3", "virtio"]
    # Using the host's resolver as a DNS proxy in NAT mode
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    # select chipset (I/O controler hub) emulation to use. ich9 may be faster
    v.customize ["modifyvm", :id, "--chipset", "ich9"]
    end

end


