# Calculate innodb-log-file-size


## Exercise (simple) 

```
pager grep sequence;
show engine innodb status; 
select sleep(60);
show engine innodb status;
```

```
mysql> select (3838334638 - 3836410803) / 1024 / 1024 as MB_per_min;
+------------+
| MB_per_min |
+------------+
| 1.83471203 | 
+------------+
```

  * https://www.percona.com/blog/how-to-calculate-a-good-innodb-log-file-size/

## Exercise 2: with sakila 

```
Open 2 sessions
Session 1: mysql to measure
Session 2: import sakila 
```

### Step 1: In Session 1 (measure) 

```
mysql
```

```
pager grep sequence;
show engine innodb status;
select sleep(120);
show engine innodb status;

```

### Step 2: In Session 2 (import sakila) 

```
cd /usr/src/sakila-db
mysql < sakila-schema.sql; mysql < sakila-data.sql;
```

### Step 3: In Session 1 (measure) - Calculate values 

```
-- Calculate values 
-- second-value-from-step1 - first-value-from-step1
-- select (second_value - first_value) / 1024 / 1024 as MB_per_2min


pager;
# eg. 312MB 
select (3838334638 - 3836410803) / 1024 / 1024 as MB_per_2min;
exit 
```

### Step 4: Adjust config accordingly 

```
# Ubuntu / Debian
cd /etc/mysql/mariadb.conf.d/
nano 50-server.cnf
```

```
# mysqld section
[mysqld]
# other settings
innodb-log-file-size=312M
```

```
systemctl restart mariadb
mysql
```

```
select @@innodb_log_file_size
# oder
show variables like '%log_file%';
exit
```
