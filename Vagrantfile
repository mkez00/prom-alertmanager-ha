# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
	config.vm.define "docker-node-1" do |c|
		c.vm.box = "ubuntu/xenial64"
  		c.vm.hostname = "docker-node-1"
  		c.vm.synced_folder "data", "/data"
  		c.vm.network "private_network", ip: "192.168.56.90"
  		c.vm.provision "shell", inline: <<-SHELL
  			sudo su
	  		apt-get update
	  		apt-get install docker.io -y

	  		# install docker compose
	  		curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
	  		chmod +x /usr/local/bin/docker-compose

	  		# create required directories and move files
	  		mkdir /etc/prometheus
	  		mkdir /var/prometheus
	  		mkdir /etc/alertmanager
	  		mkdir /var/lib/grafana

	  		# copy config files
	  		cp /data/prometheus.yml /etc/prometheus/prometheus.yml
	  		cp /data/alertmanager.yml /etc/alertmanager/alertmanager.yml
	  		cp /data/alerts.yml /var/prometheus/alerts.yml
	  		cp /data/docker-compose.yml /home/vagrant/

	  		# change permissions
	  		chmod 777 /var/prometheus/
	  		chown syslog:crontab /var/lib/grafana/

	  		# install node exporter on host
	  		mkdir /opt/prometheus
			useradd -d /opt/prometheus -U -r prometheus
			wget -O /opt/prometheus/node_exporter-0.15.2.linux-amd64.tar.gz https://github.com/prometheus/node_exporter/releases/download/v0.15.2/node_exporter-0.15.2.linux-amd64.tar.gz
			tar -zxf /opt/prometheus/node_exporter-0.15.2.linux-amd64.tar.gz -C /opt/prometheus/
			ln -s /opt/prometheus/node_exporter-0.15.2.linux-amd64/node_exporter /usr/bin/node_exporter
			cp /data/node_exporter.service /etc/systemd/system/node_exporter.service
			systemctl enable node_exporter.service
			systemctl start node_exporter.service

			# start docker compose
	  		docker-compose -f /home/vagrant/docker-compose.yml up -d

  		SHELL
	end

	config.vm.define "docker-node-2" do |c|
		c.vm.box = "ubuntu/xenial64"
  		c.vm.hostname = "docker-node-2"
  		c.vm.synced_folder "data", "/data"
  		c.vm.network "private_network", ip: "192.168.56.91"
  		c.vm.provision "shell", inline: <<-SHELL
  			sudo su
	  		apt-get update
	  		apt-get install docker.io -y

	  		# install docker compose
	  		curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
	  		chmod +x /usr/local/bin/docker-compose

	  		# create required directories and move files
	  		mkdir /etc/prometheus
	  		mkdir /var/prometheus
	  		mkdir /etc/alertmanager
	  		mkdir /var/lib/grafana

	  		# copy config files
	  		cp /data/prometheus.yml /etc/prometheus/prometheus.yml
	  		cp /data/alertmanager.yml /etc/alertmanager/alertmanager.yml
	  		cp /data/alerts.yml /var/prometheus/alerts.yml
	  		cp /data/docker-compose2.yml /home/vagrant/docker-compose.yml

	  		# change permissions
	  		chmod 777 /var/prometheus/
	  		chown syslog:crontab /var/lib/grafana/

	  		# install node exporter on host
	  		mkdir /opt/prometheus
			useradd -d /opt/prometheus -U -r prometheus
			wget -O /opt/prometheus/node_exporter-0.15.2.linux-amd64.tar.gz https://github.com/prometheus/node_exporter/releases/download/v0.15.2/node_exporter-0.15.2.linux-amd64.tar.gz
			tar -zxf /opt/prometheus/node_exporter-0.15.2.linux-amd64.tar.gz -C /opt/prometheus/
			ln -s /opt/prometheus/node_exporter-0.15.2.linux-amd64/node_exporter /usr/bin/node_exporter
			cp /data/node_exporter.service /etc/systemd/system/node_exporter.service
			systemctl enable node_exporter.service
			systemctl start node_exporter.service

			# start docker compose
	  		docker-compose -f /home/vagrant/docker-compose.yml up -d

  		SHELL
	end

	config.vm.define "worker-node" do |c|
		c.vm.box = "ubuntu/xenial64"
  		c.vm.hostname = "worker-node"
  		c.vm.synced_folder "data", "/data"
  		c.vm.network "private_network", ip: "192.168.56.92"
  		c.vm.provision "shell", inline: <<-SHELL
  			sudo su
	  		apt-get update

	  		# install node exporter on host
	  		mkdir /opt/prometheus
			useradd -d /opt/prometheus -U -r prometheus
			wget -O /opt/prometheus/node_exporter-0.15.2.linux-amd64.tar.gz https://github.com/prometheus/node_exporter/releases/download/v0.15.2/node_exporter-0.15.2.linux-amd64.tar.gz
			tar -zxf /opt/prometheus/node_exporter-0.15.2.linux-amd64.tar.gz -C /opt/prometheus/
			ln -s /opt/prometheus/node_exporter-0.15.2.linux-amd64/node_exporter /usr/bin/node_exporter
			cp /data/node_exporter.service /etc/systemd/system/node_exporter.service
			systemctl enable node_exporter.service
			systemctl start node_exporter.service
  		SHELL
	end	

end