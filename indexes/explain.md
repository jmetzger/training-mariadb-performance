# Explain verwenden 

## Einfacher Fall 

```
explain select * from actor 
```

## Erweiterter Fall
```
explain extended select * from user 
show warnings 
```

## Anzeigen der Partitions 

```
explain partitions select * from actor 
```


## Ausgabe im JSON-Format 

```
# Hier gibt es noch zusätzliche Informationen 
explain format=json select * from actor 
```
## Knoten im Taschentuch 

### bei Extras 

#### Using Index - Cover Index 

```
# z.B. select actor_id, last_name from actor;
Using index - nur den Index verwendet und kein ansonsten holt 

```

#### Using Index Condition = Index Condition Pushdown (ICP) 

```

explain extended select first_name, actor_id  from actor where last_name like 'A%';
```

![image](https://github.com/user-attachments/assets/c9efa8ea-de10-4f3d-ac9e-825e92464129)

 * https://mariadb.com/kb/en/index-condition-pushdown/

