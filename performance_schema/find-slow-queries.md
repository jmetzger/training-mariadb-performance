# Find slow queries 

## Step 1: Enable performance schema 

```
cd /etc/my.cnf.d
nano server.cnf 
```

```
[mysqld]
performance_schema=on 
```

```
#
systemctl restart mariadb
```

```
mysql -e 'select @@performance_schema' 
```

## Step 2: Activate specific settings to enable it 

```
# Instrumente aktivieren
update performance_schema.setup_instruments set enabled = 'yes', timed = 'yes';

# consumers aktiviert
# performance_schema.setup_consumers
```
![image](https://github.com/user-attachments/assets/cca55ed0-738f-45f3-8c99-8d3687eb7ec4)


```
-- Query ausgeführt:
use contributions; select * from contributions where contribution_id < 400000 and date_recieved < '2000-12-31';';
```

```
# uns in digest angeschaut
use performance_schema;
select * from events_statements_summary_by_digest \G   
# Die Laufzeit LAST_SEEN - FIRST_SEEN (Laúfzeit der Query)
# Danach könnten man sortieren  


```

## Referenz:

  * https://fromdual.com/mariadb-and-mysql-performance-schema-hints#top-long-running-queries
