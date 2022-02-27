# Klever Testnet

## Monitoring Setup
- Create a VM and install Ubuntu 20.04
- Install Docker
	- https://docs.docker.com/engine/install/ubuntu/
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
- Install Portainer
- Using Portainer, create a monitoring stack using the yml file located in this repo
- That will install the Prometheus and Grafana containers
- Edit the Prometheus config file
	- `sudo nano /etc/prometheus/prometheus.yml`
- This will configure Prometheus to target your node's metrics output location
