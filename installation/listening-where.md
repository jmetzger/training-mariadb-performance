# Where does the Server Listen 

## Step 1: Is services listening to the outside world (Ubuntu, Redhat, Rocky) ? 

```
lsof -i | grep mariadb
# localhost means it does NOT listen to the outside now 
# mariadbd  5208           mysql   19u  IPv4  56942      0t0  TCP localhost:mysql (LISTEN)

netstat -tupel 
# or 
netstat -an 

```

## Step 2: is firewall open on port 3306 or service mysql (Rocky / RHEL) 

```
firewall-cmd --list-all
# services: cockpit dhcpv6-client ssh
firewall-cmd --add-service=mysql --zone=public
firewall-cmd --runtime-to-permanent 

```


## How to fix (Ubuntu -> Mariadb Foundation) 

```
nano /etc/mysql/mariadb.conf.d/50-server.cnf
```

```
# In Section [mysqld] 
# Change bind-address to -> bind-address = 0.0.0.0
[mysqld]
bind-address = 0.0.0.0
```

```
systemctl restart mariadb
systemctl status mariadb
lsof -i 
```

## Can I bind to multiple addresses  ?

```
# from 10.11 it is possible, before not, you have to use 0.0.0.0
Starting with MariaDB 10.11, a comma-separated list of addresses to bind to can be given.
```

 * https://mariadb.com/kb/en/server-system-variables/#bind_address
