# Unifi
Unifi Controller Configuration

### Prerequisistes
- Docker
- Docker Compose
- UFW(Firewall)

#### Docker
See [Ubuntu Docs](https://docs.docker.com/engine/install/ubuntu/) or [Debian Docs](https://docs.docker.com/engine/install/debian/)

#### Docker Compose
See [Install Docs](https://docs.docker.com/compose/install/). *If running on Raspberry PI (ARM) install from apt repo*
```
$ sudo apt install docker-compose
```

#### UFW Firewall
```
$ sudo apt install ufw
$ sudo ufw enable 22
```

### Firewall Configuration
Copy the included ufw_unifi rules file into ufw application directory
```
$ /etc/ufw/applications.d
```
then enable the rules
```
$ sudo ufw app update unifi_rules
$ sudo ufw allow Unifi
```

### Unifi Docker Configuration
```
$ sudo mkdir /apps/unifi/config
$ sudo chmod -R johnsoga:johnsoga: /apps
$ cd /apps/unifi
$ git clone https://github.com/johnsoga/unifi .
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
