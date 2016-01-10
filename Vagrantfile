Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/vivid64"

  config.vm.network :private_network, ip: "192.168.10.11", netmask: "255.255.255.0"

  config.hostmanager.aliases = %w(admin-my.zanichelli.local cdn-my.zanichelli.local my.zanichelli.local api-my.zanichelli.local dev.myzanichelli.local)
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true

  config.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.customize ["modifyvm", :id, "--memory", "2048"]
      vb.customize ["modifyvm", :id, "--cpus", "1"]
      vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  config.vm.synced_folder "~/.ssh",
    "/home/vagrant/keys/"
  config.vm.synced_folder "../ir-lucene",
    "/home/vagrant/project/ir-lucene"

  config.vm.provision :ansible_local do |ansible|
    #ansible.verbose = "v"
    ansible.playbook = "playbook.yml"
    ansible.install = true
    ansible.version = "latest"
  end
end