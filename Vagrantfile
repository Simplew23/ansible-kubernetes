# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
hosts = YAML.load_file('hosts.yml')

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.box_check_update = false

  hosts.each do |host|
    config.vm.define host["name"] do |srv|
      srv.vm.network :private_network, :ip => host["ip1"]
      srv.vm.hostname = host["name"]
    
      srv.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.memory = host["memory"]
        vb.cpus = host["cpu"]
      end

      srv.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~vagrant/.ssh/me.pub"

      srv.vm.provision "shell", inline: <<-SHELL
        cat ~vagrant/.ssh/me.pub >> ~vagrant/.ssh/authorized_keys

        useradd -m teligent
        sudo mkdir ~teligent/.ssh
        sudo cat ~vagrant/.ssh/me.pub >> ~teligent/.ssh/authorized_keys
        sudo chmod 700 ~teligent/.ssh
        sudo chmod 600 ~teligent/.ssh/*
        sudo chown -R `id -u teligent`:`id -g teligent` ~teligent/.ssh

        echo '%teligent ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/teligent
      SHELL

      srv.vm.provision "shell", inline: <<-SHELL
        curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.rpm.sh | sudo bash
        sudo yum install gitlab-runner -y
      SHELL
    end
  end
end
