# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
    
   config.vm.define "server" do |server| 
   server.vm.box = "sbeliakou/centos-7.4-x86_64-minimal"
   server.vm.hostname = "server"
   server.vm.network "private_network", ip: "192.168.56.100"
   server.vm.network "private_network", ip: "192.168.56.101"
   server.vm.provider 'virtualbox' do |vb|
        vb.memory="2048"  
	vb.name = "server"
   end
   server.vm.provision 'shell', inline: <<-EOF

	yum install -y epel-release wget net-tools
	yum install -y java-devel
	yum install -y nginx
	systemctl start nginx
	sed -i '/^        location \/ {/a \  proxy_pass http:\/\/192.168.56.100:8080;' /etc/nginx/nginx.conf
	systemctl restart nginx
	wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war
	nohup java -jar jenkins.war &

    
    
  EOF
  end




  
end
