Vagrant.configure("2") do |config|

  config.vm.define "victima" do |victima|
    victima.vm.box = "debian/jessie64"
    victima.vm.synced_folder ".", "/vagrant", disabled: true
    victima.vm.network "private_network", type: "dhcp",
    	name: "vboxnet0" 
    victima.vm.provider "virtualbox" do |vb|	
	vb.memory = "2048"
    end
    victima.vm.provision "shell",
	    inline: "apt update && apt install -y --no-install-recommends tcpdump hping3"
  end  

  config.vm.define "atacante" do |atacante|
    atacante.vm.box = "debian/jessie64"
    atacante.vm.synced_folder ".", "/vagrant", disabled: true
    atacante.vm.network "private_network", type: "dhcp",
    	name: "vboxnet0"
    atacante.vm.provider "virtualbox" do |vb|	
	vb.memory = "2048"
    end
    atacante.vm.provision "shell",
	    inline: "apt update && apt install -y --no-install-recommends tcpdump hping3"
  end  
  
  config.vm.define "zombie" do |zombie|
    zombie.vm.box = "matthewjberger/win7-64-en"
    zombie.vm.guest = :windows
    zombie.vm.box_version = "1.0.0"
    zombie.vm.boot_timeout = 600
    zombie.vm.synced_folder ".", "/vagrant", disabled: true
    zombie.vm.provider "virtualbox" do |vb|	
	vb.gui = true
	vb.memory = "2048"
    end
    zombie.ssh.insert_key = false
  end
 
end
