# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_NAME = "ubuntu-12.04"
BOX_URL  = "https://s3-us-west-2.amazonaws.com/squishy.vagrant-boxes/precise64_squishy_2013-02-09.box"

Vagrant.configure("2") do |config|
  config.vm.box = ENV.fetch("ROM_VAGRANT_BOX", BOX_NAME)
  config.vm.box_url = ENV.fetch("ROM_VAGRANT_URL", BOX_URL)
  config.vm.hostname = 'rom-rb'
  #config.vbguest.auto_update = true
  config.ssh.forward_agent = true

  if File.file? (File.expand_path '~/vagrant_setup.rb')
    require '~/vagrant_setup.rb'
  else 
    require 'ostruct'
    USER_CONFIG = OpenStruct.new(data_dir: (File.expand_path '~'))
  end

  # Share folder configuration
  if USER_CONFIG.data_dir
     config.vm.synced_folder USER_CONFIG.data_dir, "/host_folder"
  end 

  if rom_dotfiles = ENV.fetch('ROM_DOTFILES', false)
    config.vm.synced_folder rom_dotfiles, "#{USER_CONFIG.data_dir}/.dotfiles"
  end

  config.vm.provision :chef_solo do |chef|
    chef.add_recipe 'main'
  end
end
