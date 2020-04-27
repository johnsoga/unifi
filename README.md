# Unifi
Unifi Controller Configuration

### Prerequisistes
- Docker
- Docker Compose
- UFW(Firewall)

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

### Running
```
$ docker pull linuxserver/unifi-controller
$ XUID=$(id -u $USER) XGID=$(id -g $USER) docker-compose up -d
```
