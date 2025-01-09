# Install percona - toolkit 

## Walkthrough Rocky 9 / RHEL 9 

```
wget https://downloads.percona.com/downloads/percona-toolkit/3.7.0/binary/redhat/9/x86_64/percona-toolkit-3.7.0-1.el9.x86_64.rpm

dnf localinstall percona-toolkit-3.7.0-1.el9.x86_64.rpm
```


## Walkthrough (Ubuntu 20.04) 

```
# Howto 
# https://www.percona.com/doc/percona-toolkit/LATEST/installation.html

# Step 1: repo installieren mit deb -paket 
wget https://repo.percona.com/apt/percona-release_latest.focal_all.deb
apt update 
apt install -y curl 
dpkg -i percona-release_latest.focal_all.deb
apt update
apt install -y percona-toolkit 
```

## Walkthrough (Debian 10) 

```
sudo apt update
sudo apt install -y wget gnupg2 lsb-release curl
cd /usr/src 
wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb
dpkg -i percona-release_latest.generic_all.deb
apt update
apt install -y percona-toolkit 
```

```
sudo apt update; sudo apt install -y wget gnupg2 lsb-release curl; cd /usr/src; wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb; dpkg -i percona-release_latest.generic_all.deb; apt update; apt install -y percona-toolkit 
```
