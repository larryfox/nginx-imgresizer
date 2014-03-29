# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'precise64'
  config.vm.box_url = 'http://files.vagrantup.com/precise64.box'

  config.vm.hostname = 'imgresizer.local'

  config.vm.synced_folder '.', '/var/www/imgresizer/public'

  config.vm.network :private_network, ip: '192.168.60.40'
  config.vm.network :forwarded_port, guest: 443, host: 8888

  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'provisioning/site.yml'
    ansible.verbose = 'v'
    ansible.inventory_path = 'provisioning/development'
  end

  config.vm.provider :virtualbox do |vb|
    vb.customize ['modifyvm', :id, '--memory', '1024']
  end
end
