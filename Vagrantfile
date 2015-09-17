# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: "192.168.33.100"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "768"
  end
  config.vm.provision "shell", inline: <<-SHELL

    sudo apt-get update
    sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
    sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install vim mysql-server-5.6 -y
    sed -i "s/^bind-address/#bind-address/" /etc/mysql/my.cnf
    mysql -u root -proot -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION; FLUSH PRIVILEGES;"
    sudo /etc/init.d/mysql restart    
  SHELL
end
