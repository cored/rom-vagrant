# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = ENV.fetch("ROM_VAGRANT_BOX")
  config.vm.hostname = 'rom-rb'
  config.vbguest.auto_update = true
  config.ssh.forward_agent = true

  config.vm.synced_folder ENV.fetch('ROM_ROOT'), '/home/vagrant/rom-rb'

  if rom_dotfiles = ENV.fetch('ROM_DOTFILES', false)
    config.vm.synced_folder rom_dotfiles, '/home/vagrant/.dotfiles'
  end

  config.vm.provision :chef_solo do |chef|
    chef.add_recipe 'main'
  end
end
