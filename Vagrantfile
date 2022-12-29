
Vagrant.configure("2") do |config|
#ansible-node1
 config.vm.define:"ansible-node1" do |cfg|
  # boxes at https://vagrantcloud.com/search.
    cfg.vm.box = "centos/7"
    cfg.vm.provider:virtualbox do |vb|
	  vb.name="Ansible-Node1"
	  vb.customize ["modifyvm", :id, "--cpus",1]
	  vb.customize ["modifyvm", :id, "--memory",512]
	end
	cfg.vm.host_name="ansible-node1"
    cfg.vm.synced_folder ".", "/vagrant", disabled: true
	cfg.vm.network "public_network", ip: "192.168.1.11"
	cfg.vm.network "forwarded_port", guest: 22, host: 19211, auto_correct: false, id: "ssh"
	#cfg.vm.provision "shell", path: "bootstrap.sh"
	cfg.vm.provision "shell", path: "bash_ssh_conf_4_CentOS.sh"
  end
  
  # /mnt mount error 발생 시 
  # vagrant plugin uninstall vagrant-vbguest 
  # vagrant plugin install vagrant-vbguest --plugin-version 0.21 

#ansible-node2
 config.vm.define:"ansible-node2" do |cfg|
  # boxes at https://vagrantcloud.com/search.
    cfg.vm.box = "centos/7"
    cfg.vm.provider:virtualbox do |vb|
	  vb.name="Ansible-Node2"
	  vb.customize ["modifyvm", :id, "--cpus",1]
	  vb.customize ["modifyvm", :id, "--memory",512]
	end
	cfg.vm.host_name="ansible-node2"
    cfg.vm.synced_folder ".", "/vagrant", disabled: true
	cfg.vm.network "public_network", ip: "192.168.1.12"
	cfg.vm.network "forwarded_port", guest: 22, host: 19212, auto_correct: false, id: "ssh"
	#cfg.vm.provision "shell", path: "bootstrap.sh"
	cfg.vm.provision "shell", path: "bash_ssh_conf_4_CentOS.sh"
  end


  config.vm.define:"ansible-server" do |cfg|
  # boxes at https://vagrantcloud.com/search.
    cfg.vm.box = "centos/7"
    cfg.vm.provider:virtualbox do |vb|
	  vb.name="Ansible-Server"
	end
	cfg.vm.host_name="ansible-server"
    cfg.vm.synced_folder ".", "/vagrant", disabled: true
	cfg.vm.network "public_network", ip: "192.168.1.10"
	cfg.vm.network "forwarded_port", guest: 22, host: 19210, auto_correct: false, id: "ssh"
	cfg.vm.provision "shell", path: "bootstrap.sh"
	cfg.vm.provision "file", source: "Ansible_env_ready.yml", destination: "Ansible_env_ready.yml"
	cfg.vm.provision "shell", inline: "ansible-playbook Ansible_env_ready.yml"
	cfg.vm.provision "shell", path: "add_ssh_auth.sh", privileged: false
	cfg.vm.provision "file", source: "Ansible_ssh_conf_4_CentOS.yml", destination: "Ansible_ssh_conf_4_CentOS.yml"
	cfg.vm.provision "shell", inline: "ansible-playbook Ansible_ssh_conf_4_CentOS.yml"
  end

end

