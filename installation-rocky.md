# Installation Rocky 9
## Setup repo and install

 * https://downloads.mariadb.org/mariadb/repositories/

```
sudo su -
cd /etc/yum.repos.d
nano mariadb.repo
```

```
# MariaDB 10.6 RedHatEnterpriseLinux repository list - created 2025-01-08 10:52 UTC
# https://mariadb.org/download/
[mariadb]
name = MariaDB
# rpm.mariadb.org is a dynamic mirror if your preferred mirror goes offline. See https://mariadb.org/mirrorbits/ for details.
# baseurl = https://rpm.mariadb.org/10.6/rhel/$releasever/$basearch
baseurl = https://ftp.agdsn.de/pub/mirrors/mariadb/yum/10.6/rhel/$releasever/$basearch
# gpgkey = https://rpm.mariadb.org/RPM-GPG-KEY-MariaDB
gpgkey = https://ftp.agdsn.de/pub/mirrors/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck = 1
```

```
dnf install -y MariaDB-server MariaDB-client
```



## Check if running and enabled 

```
systemctl status mariadb
systemctl start mariadb
systemctl enable mariadb
systemctl status mariadb 
# enabled, wenn in Zeile 2 mariadb.service;enabled; auftaucht 
```


## Secure installation 

```
mariadb-secure-installation
```
# OR: if not present before 10.4 
mysql_secure_installation 
```
