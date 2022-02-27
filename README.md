# klever-testnet

## Setup
- Create a VM and install Ubuntu 20.04
- Install Docker
	- https://docs.docker.com/engine/install/ubuntu/
- Install Docker Compose
- Install Portainer
- Using Portainer, create a monitoring stack using the yml file located in this repo
- That will install the Prometheus and Grafana containers
- Edit the Prometheus config file
	- `sudo nano /etc/prometheus/prometheus.yml`
- This will configure Prometheus to target your node's metrics output location