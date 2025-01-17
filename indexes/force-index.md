# Sometimes you need to force an index 

## In Order By an index is often not used .

  * https://mariadb.com/kb/en/index-hints-how-to-force-query-plans/#force-index-forcing-an-index

## Use data from contributions 

### Walkthrough 

```
mysql contributions 
```

```
# Set an index
create index idx_contributions_date_recieved on contributions (date_recieved);
```

```
# order by without index (decides to use table scan)
explain select * from contributions order by date_recieved desc limit 100000;
```

![image](https://github.com/user-attachments/assets/f5947f26-d2be-4c68-9b80-8ef14933327e)

```
explain select * from contributions force index (idx_contributions_date_recieved) order by date_recieved desc limit 100000;
```

![image](https://github.com/user-attachments/assets/28d251b3-4268-441c-8409-32509a63ca71)

```
# how long does it take ? without index
select * from contributions order by date_recieved desc limit 100000;
```
![image](https://github.com/user-attachments/assets/289b679c-280f-492c-9d19-ace3d4f20b85)

```
# Now forcing the index
select * from contributions force index (idx_contributions_date_recieved) order by date_recieved desc limit 100000;
```

![image](https://github.com/user-attachments/assets/c2396575-e153-4415-84a6-11a37e782497)
