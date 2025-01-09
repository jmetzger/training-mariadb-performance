# Slow Query Log

## Variante 1: Langsame Queries loggen

### Step 1: Config vorbereiten 

```
nano /etc/my.cnf.d/server.cnf
```

```
# unterhalb von [mysqld]
# guter richtwert 
# long_query_time=0.5

# nur fürs Training um Daten zu bekommen
long_query_time=0.000001
```

```
systemctl restart mariadb
```

### Step 2: Während der Laufzeit global aktivieren 

```
mysql
```

```
set global slow_query_log = 1;
```

```
## Wichtig: Ist jetzt erst beim nächsten Connection mit einer Session für diese Session aktiv
```

### Step 3: Zusätzliche sinnvolle Einstellungen vornehmen für das slow_query_log


#### bis Version 10.4 (inkl.)

```
# Alle Logs analysieren, die kein Index verwendet 
#/etc/mysql/mariadb.conf.d/50-server.cnf 
# unter [mysqld]

# slow query log 
slow-query-log
log-queries-not-using-indexes
log-slow-rate-limit=5
log-slow-verbosity = 'query_plan,explain'
```
#### ab Version 10.6. (auf Rocky / RHEL)

```
# Empfehlung in der config
nano /etc/my.cnf.d/server.cnf
```

```
# alle queries loggen die kein index haben
log-queries-not-using-indexes
# das nur für production, wenn wirklich dort getracked werden soll 
# nur jede 2. mitloggen 
log-slow-rate-limit=20
# hier nimmt er alle optionen als Zusatzinformationen
# auch neu (ab. 10.6: engine, Innodb
log-slow-verbosity=All
```

```
systemctl restart mariadb
```





## Variante 1: Aktivieren (minimum) 

```
# auch direkt in 50-server.cnf möglich 
mysql>set global long_query_time=0.5 # 0,5 Sekunden. Alles was >= 0,5 sekunden dauert, wird geloggt 
mysql>set session long_query_time=0.5
mysql>set global slow_query_log=1 
mysql>set session slow_query_log=1 
```

## Logge alles wo kein Index verwendet werden kann (egal) wie langsam oder schnell 

```
# damit er wirklich nur die queries logged, die keinen index haben, sollte. der 
# long_query_time - Wert möglichst hoch sein. 
set global long_query_time = 20 
set session long_query_time = 20
set global slow_query_log = 1
set session slow_query_log = 1 
set global log_queries_not_using_indexes = 1
set session log_queries_not_using_indexes = 1 

```

## Bitte slow_query_log bei der ausgabe geschätziger zu sein

```
set global log_slow_verbosity = 'query_plan,explain'
set session log_slow_verbosity = 'query_plan,explain'

```

## Die Anzahl der Ausgabe reduzieren (nur jedes 5.) 

```
## /etc/mysql/mariadb-conf.d/50-server.cnf und mysqld 
log-slow-rate-limit=5;
```




## Ref: 

 * https://mariadb.com/kb/en/slow-query-log-overview/
