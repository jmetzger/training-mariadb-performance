# Installation Rocky 9
## Setup repo and install

 * https://downloads.mariadb.org/mariadb/repositories/

```
## repo 
sudo apt-update 
sudo apt-get install software-properties-common dirmngr
sudo apt-key adv --fetch-keys 'https://mariadb.org/mariadb_release_signing_key.asc'
sudo add-apt-repository 'deb [arch=amd64,arm64,ppc64el] http://mirror2.hs-esslingen.de/mariadb/repo/10.5/debian buster main'
## now update and install 
sudo apt update
sudo apt install mariadb-server 

```

## Check if running and enabled 

```
systemctl status mariadb 
# enabled, wenn in Zeile 2 mariadb.service;enabled; auftaucht 
```


## Secure installation 

```
mariadb-secure-installation 
# OR: if not present before 10.4 
mysql_secure_installation 
```
