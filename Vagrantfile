$script_mysql = <<-SCRIPT
  apt-get update && \
  apt-get install -y mysql-server-5.7 && \
  mysql < /vagrant/mysql/script/user.sql && \
  mysql < /vagrant/mysql/script/schema.sql && \]
  mysql < /vagrant/mysql/script/data.sql && \
  cat /vagrant/mysql/mysqld.cnf > /etc/mysql/mysql.conf.d/mysqld.cnf && \
  service mysql restart
SCRIPT

#Vagrant config
Vagrant.configure("2") do |config|

  #VM base
  config.vm.box = "ubuntu/bionic64"

  # Provider specific
  config.vm.provider "virtualbox" do |vb|
    # Customize the number of cpu on the VM:
    vb.cpus = 1
    # Customize the amount of memory on the VM:
    vb.memory = 1024
  end

  #MySql Config
  config.vm.define "mysql" do |mysqlserver|
    mysqlserver.vm.network "private_network", ip: "10.80.4.10"
    mysqlserver.vm.network "forwarded_port", guest: 3306, host: 3306

    mysqlserver.vm.provider "virtualbox" do |vb|
      vb.name = "mysql"
    end
    # Enable provisioning with a shell script.
    mysqlserver.vm.provision "shell", inline: $script_mysql
  end
end
