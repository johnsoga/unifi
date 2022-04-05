# Unifi
Unifi Controller Configuration

### Prerequisistes
- [Docker](https://docs.docker.com/engine/)
- [Docker Compose](https://docs.docker.com/compose/)
- [UFW(Firewall)](https://en.wikipedia.org/wiki/Uncomplicated_Firewall)
- [Docker Image](https://docs.linuxserver.io/images/docker-unifi-controller)

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
```shell
sudo mkdir /apps/docker/unifi/config
sudo chmod -R johnsoga:johnsoga: /apps
cd /apps/docker/unifi
git clone https://github.com/johnsoga/unifi .
```

### Running
```
$ cd /apps/unifi
$ docker pull linuxserver/unifi-controller
$ XUID=$(id -u $USER) XGID=$(id -g $USER) docker-compose up -d unifi-controller
```

### Updates
```
$ cd /apps/unifi
$ XUID=$(id -u $USER) XGID=$(id -g $USER) docker-compose pull unifi-controller
```
