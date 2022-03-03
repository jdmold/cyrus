# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "ansbl", primary: true do |ansbl|
    config.vm.hostname = "ansbl"
    ansbl.vm.box = "centos/7"
    ansbl.vm.network "private_network", type: "dhcp"

    ansbl.vm.provider "virtualbox" do |vb|
      # Customize the amount of memory on the VM:
      vb.memory = "1024"
    end
    ansbl.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/id_rsa.pub", run: "always"
    ansbl.vm.provision "file", source: "~/.ssh/id_rsa", destination: "/home/vagrant/.ssh/id_rsa", run: "always"
    ansbl.vm.provision :shell, :inline => "cat /home/vagrant/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys", run: "always"

    # ansbl.vm.synced_folder "../data", "/vagrant_data"
    ansbl.vm.provision "shell", inline: <<-SHELL
      yum update -y
      yum install -y epel-release
      yum makecache fast
      yum install -y python3
    SHELL
  end
end

vagrantfiles = %w[vagrant/Vagrantfile.centos-7-a vagrant/Vagrantfile.centos-8-a]
# vagrantfiles = %w[vagrant/Vagrantfile.*]
vagrantfiles.each do |vagrantfile|
  load File.expand_path(vagrantfile) if File.exists?(vagrantfile)
end
