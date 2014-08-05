# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "chef/ubuntu-13.10"
  config.berkshelf.enabled = true

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.

  # Nginx
  config.vm.network "forwarded_port", guest: 80, host: 8080

  # Nginx status
  config.vm.network "forwarded_port", guest: 8090, host: 8090

  # ElasticSearch (This is just for testing purposes; remove when Kibana configured)
  config.vm.network "forwarded_port", guest: 9200, host: 9200

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Don't boot with headless mode
  #   vb.gui = true
  #
  #   # Use VBoxManage to customize the VM. For example to change memory:
  #   vb.customize ["modifyvm", :id, "--memory", "1024"]
  # end
  #
  # View the documentation for the provider you're using for more
  # information on available options.

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  # Info:
  #   https://docs.vagrantup.com/v2/provisioning/chef_common.html
  #   https://docs.vagrantup.com/v2/provisioning/chef_solo.html

  config.omnibus.chef_version = :latest

  config.vm.provision "chef_solo" do |chef|
  #   chef.cookbooks_path = "../my-recipes/cookbooks"
     chef.roles_path = "./roles"
  #   chef.data_bags_path = "../my-recipes/data_bags"

     # https://github.com/opscode-cookbooks/apt
     chef.add_recipe "apt"
    
     # https://github.com/opscode-cookbooks/vim
     chef.add_recipe "vim"

     # https://github.com/agileorbit-cookbooks/java
     chef.add_recipe "java"

     # https://github.com/elasticsearch/cookbook-elasticsearch
     #chef.add_recipe "elasticsearch"

     # https://github.com/miketheman/nginx
     #chef.add_recipe "nginx"

     # https://github.com/lusis/chef-kibana
     #chef.add_recipe "kibana::install"

     #chef.add_role "elasticsearch_server"
     #chef.add_role "logstash_server"
     chef.add_recipe "logstash::server"
     chef.add_recipe "logstash::agent"
     chef.add_recipe "logstash::kibana"

  #   chef.add_role "web"
  #
     # You may also specify custom JSON attributes:
     chef.json = {
                   #"name" => "elasticsearch_test_elk",
                   "java" => {
                     "jdk_version" => "7"
                   },
                   #"elasticsearch" => {
                   #  "cluster" => {
                   #    "name" => "elasticsearch_test_elk"
                   #  }
                   #},
                   #"kibana" => {
                     #"webserver" => "nginx"
                   #},
                   "logstash" => {
                   #  "server" => {
                   #    "enabled" => true
                     #},
                     "instance" => {
                       "name" => "default"
                     #},
                     #"input" => {
                     #  "file" =>  {
                     #    "path" => "/home/vagrant/server_logs",
                     #    "type" => 
                     #  }
                     }
                   }
                 }
  end

end
