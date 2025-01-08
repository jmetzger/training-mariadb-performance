# Where does the Server Listen 

## How to check ? 

```
lsof -i | grep mariadb
# localhost means it does NOT listen to the outside now 
# mariadbd  5208           mysql   19u  IPv4  56942      0t0  TCP localhost:mysql (LISTEN)

netstat -tupel 
# or 
netstat -an 

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
