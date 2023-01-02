Vagrant.configure("2") do |config|

  #BASE CONFIGURATION

  config.vm.box = "ffw-drupal10"

  config.vm.define "ffw-drupal10"

  # NETWORKING CONFIGURATION

  config.vm.network 'private_network', ip: '192.168.33.3'

  config.vm.network "public_network"


  config.vm.network "forwarded_port", guest: 80, host: 8091

  # SSH CONFIGURATION

  config.ssh.insert_key = false

  config.ssh.private_key_path = "./.ssh/ffw-custom-key"

  config.ssh.forward_agent = true


  #SYNC FOLDER / MOUNT CONFIGURATION

  #sync drupal into var/www directory so it can be used by Apache VH.
  config.vm.synced_folder "./drupal-dir/", "/var/www/drupal-10", create: true,
  owner: "vagrant", group: "vagrant"

  #sync ansible files inside the vm
  config.vm.synced_folder "./.ansible/", "/vagrant/.ansible", create: true

  # disable the default vagrant folder sync
  config.vm.synced_folder ".", "/vagrant", disabled: true


  # config.vm.network "public_network"
  # config.vm.synced_folder "./", "/", create: true

  #PROVISION CONFI  GURATION

  # ANSIBLE 
  config.vm.provision :ansible_local do |ansible|
    ansible.playbook = ".ansible/playbook.yml"
    ansible.inventory_path = '.ansible/inventory'
    ansible.limit = 'all'
  end

end