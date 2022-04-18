# Unifi
Unifi Controller Configuration

### Prerequisistes
- [Docker](https://docs.docker.com/engine/)
- [Docker Compose](https://docs.docker.com/compose/)
- [UFW(Firewall)](https://en.wikipedia.org/wiki/Uncomplicated_Firewall)
- [Docker Image](https://docs.linuxserver.io/images/docker-unifi-controller)

### DHCP Server
In the DHCP Server settings for the interface that the Unifi Controller is connected to be sure to enable [DHCP Option 43](https://datatracker.ietf.org/doc/html/rfc2132#section-8.4). This essentially will allow additional devices to know how to contact the Unifi Controller for Adoption. This [site](https://tcpip.wtf/en/unifi-l3-adoption-with-dhcp-option-43-on-pfsense-mikrotik-and-others.htm) can help calculate/convert the information needed for use with pfSense as well as other manufacturers 

### Docker Installation
#### Docker
See [Ubuntu Docs](https://docs.docker.com/engine/install/ubuntu/) or [Debian Docs](https://docs.docker.com/engine/install/debian/)

#### Docker Compose
See [Install Docs](https://docs.docker.com/compose/install/)

### Firewall Configuration
#### UFW Firewall
This installs and enables the firewall (default: block all incoming) and then opens port for SSH access so we don't lose access to the server
```shell
sudo apt install ufw
sudo ufw allow OpenSSH
sudo ufw enable
```
#### Unifi Rules
Copy the included ufw firewall rules from the ufw_unifi file into a new file in the ufw application directory. This will open all the ports utilized by the Unifi Controller as documented [here](https://help.ui.com/hc/en-us/articles/218506997-UniFi-Ports-Used)
```shell
cd /etc/ufw/applications.d
sudo vim unifi
```
then enable the rules
```shell
sudo ufw app update unifi
sudo ufw allow Unifi
```

### Unifi Docker Configuration
Copy the contents of the `docker-compose.yaml` file into your `docker-compose.yaml` file. Depending on your use case you may have the Unifi Controller listening on the default machine interface IP in which case you can remove `[IP_ADDR]:` from the relevant lines as you only need to map the ports and not to a specific IP address. 
```shell
sudo mkdir /apps
sudo chmod -R johnsoga:johnsoga: /apps
mkdir /apps/docker/unifi
vim docker-compose.yaml
```

### Running
```shell
cd /apps/docker/unifi
XUID=$(id -u $USER) XGID=$(id -g $USER) docker pull
XUID=$(id -u $USER) XGID=$(id -g $USER) docker compose up -d
```

### Updates
```shell
cd /apps/docker/unifi
XUID=$(id -u $USER) XGID=$(id -g $USER) docker-compose pull
```
