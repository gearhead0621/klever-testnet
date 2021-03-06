# Klever Testnet

## Monitoring Setup
- Create a VM and install Ubuntu 20.04
### Docker Install
- Install Docker
	- Install necessary packages
		- `sudo apt-get install ca-certificates curl gnupg lsb-release`
	- Add Docker's GPG key
		- `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg`
	- Setup stable repo
		- `echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`
	- Update and install Docker
		- `sudo apt update`
		- `sudo apt-get install docker-ce docker-ce-cli containerd.io`
	- Verify installation
		- `sudo docker run hello-world`

### Post-install steps
- Create docker group
	- `sudo groupadd docker`
- Add your user to docker group
	- `sudo usermod -aG docker $USER`
- Log out and back in so your group membership is re-evaluated (if on a VM it may need to be restarted)
	- On Linux you can also use `newgrp docker` to activate the changes to groups
- Verify you can run docker commands without sudo
	- `docker run hello-world`

### Docker Compose Install
- Install Docker Compose
	- Using the linuxserver.io docker-compose image
		- `sudo curl -L --fail https://raw.githubusercontent.com/linuxserver/docker-docker-compose/master/run.sh -o /usr/local/bin/docker-compose`
		- `sudo chmod +x /usr/local/bin/docker-compose`
	- Update the local image
		- `docker pull linuxserver/docker-compose:"${DOCKER_COMPOSE_IMAGE_TAG:-latest}"`
		- `docker image prune -f`
	- Test installation
		- `docker-compose --version`
	- Create docker-compose.yml file (typically stored in the /opt directory)
		- `sudo nano /opt/docker-compose.yml`

### Monitoring Container Setup
- Install Portainer
	- Copy the settings from the portainer.yml file in this repo into your docker-compose.yml file
- Run your container
	- `cd /opt`
	- `docker-compose pull`
	- `docker-compose up -d`
- Navigate to the Portainer instance in your browser http://yourip:9000
- Portainer will have you create a username and password upon first login
- Since we are running Portainer on the VM we are going to use for the monitoring setup, you can select the local Docker enviornment
- Using Portainer, create a monitoring stack using the monitoring.yml file located in this repo
	- That will install the Prometheus, Grafana, and Alertmanager containers
	- Edit the Prometheus config file
		- `sudo nano /etc/prometheus/prometheus.yml`
	- You can use the example yml in this repo
- This will configure Prometheus to target your node's metrics output location
- When configured correctly you should see an output on the Targets tab of your Prometheus instance that looks like this:
![alt text](https://github.com/gearhead0621/klever-testnet/blob/main/images/Prometheus%20Targets%20example.png "Logo Title Text 1")

### Node Exporter & cAdvisor
- You can use Portainer to manage remote systems as well
- You will need to install Portainer Agent on the remote system, in this case it should be your Klever Testnet node
- Once installed, you can configure it in Portainer
- Create a new stack so you can install Node Exporter and cAdvisor
	- Copy the node-exporter.yml file in this repo
	- We will use port 8081 for cAdvisor since 8080 is used by the node (thanks [Klevernator](https://github.com/KingStake21) for this tip!)
### Grafana Dashboard configuration

