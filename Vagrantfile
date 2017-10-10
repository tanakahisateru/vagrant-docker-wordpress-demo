# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  #config.vm.box = "base"

  config.vm.define "db" do |db|
    db.vm.provider "docker" do |d|
      d.name = "vddb"
      d.image = "mysql:latest"
      d.env = {
        "MYSQL_ROOT_PASSWORD": "rootpass"
      }
    end
    db.vm.synced_folder "./mysql", "/var/lib/mysql"
  end

  config.vm.define "wp" do |wp|
    wp.vm.provider "docker" do |d|
      d.name = "vdwp"
      d.image = "wordpress:latest"
      d.link "vddb:mysql"
    end
    wp.vm.network :forwarded_port, guest: 80, host: 8080
    wp.vm.synced_folder "./wp-content", "/var/www/html/wp-content"
  end

end
