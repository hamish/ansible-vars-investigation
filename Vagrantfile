# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

  config.vm.define 'build' do |machine|
    machine.vm.box = "bento/centos-7.2"
    machine.vm.provision "shell", inline: <<-SHELL
      # Install ansible and allow the vagrant user to ssh to localhost
      yum install epel-release -y
      yum --enablerepo=epel install git ansible sshpass rsync-y
      cat /dev/zero | su - vagrant -c "ssh-keygen -q -N '' -C 'Keypair for Ansible' "
      ssh-keyscan localhost | su - vagrant -c 'tee -a /home/vagrant/.ssh/known_hosts'
      su - vagrant -c 'sshpass -p vagrant ssh-copy-id localhost'

    SHELL
  end 
end
