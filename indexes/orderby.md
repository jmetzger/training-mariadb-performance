# Using index for order by 

## you can use a multi-column index, but first fields needs to be static 

```
explain select * from actor where last_name = 'Akroyd' order by first_name desc;
```

![image](https://github.com/user-attachments/assets/8144dda3-2edc-4a5d-ab35-edbb4c910d7b)

## When it is not static, it does not work (filesort is used) 

```
select * from actor where last_name like 'Ak%' order by first_name desc;
```

![image](https://github.com/user-attachments/assets/3269ff83-f00d-455e-9707-9f9b7cb79dff)

## You can use an index solely on order by but optimizer decided, if it uses it.

