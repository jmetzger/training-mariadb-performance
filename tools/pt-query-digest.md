# pt-query-digest 

## Requires

  * Install percona-toolkit 
  
## Prepare: Activate slow quer log 

```
# first enable slow_query_log 
set global slow_query_log = on 
set global long_query_time = 0.2 
# to avoid, that i have to reconnect with new session 
set session long_query_time = 0.2 

# produce slow query - for testing 
select * from contributions where vendor_last_name like 'W%';
mysql > quit 
```


## Analyze: slow_query_log 

```

cd /var/lib/mysql 
# look for awhile wih -slow.log - suffix 
pt-query-digest mysql-slow.log > /usr/src/report-slow.txt
cd /usr/src 
less report-slow.txt 

```
