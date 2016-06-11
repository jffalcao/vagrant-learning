
Vagrant.configure(2) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  #config.vm.provision "chef_solo", run_list: ['vagrant-learning']
  config.vm.provision "chef_solo" do |chef|
    chef.add_recipe "vagrant-learning"
  end
end
