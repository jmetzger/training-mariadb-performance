# Force the wrong index 

   * Sometimes you force the wrong index
   * You will have penalty on your time
   * Here is an example

## Using contributions 

```
# if not created in example before,please create
create index idx_contributions_date_recieved on contributions (date_recieved); 
```

```
# Do what the optimizer wants
explain select * from contributions where contribution_id < 400000 and date_recieved < '2000-12-31';
select * from contributions where contribution_id < 400000 and date_recieved < '2000-12-31';
```

![image](https://github.com/user-attachments/assets/804c1be1-52f5-454d-a5cb-c38b2bace278)



```
# Forcing the index, performance is worse
explain select * from contributions force index (idx_contributions_date_recieved) where contribution_id < 400000 and date_recieved < '2000-12-31';
select * from contributions force index (idx_contributions_date_recieved) where contribution_id < 400000 and date_recieved < '2000-12-31';
```

![image](https://github.com/user-attachments/assets/23b3f9de-0dd0-47d7-9364-815ddd2439d6)
