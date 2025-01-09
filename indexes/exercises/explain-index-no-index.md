# Explain index, no index 

```
create table actorneu as select * from actor
```

```
# Ausgabe mit Nutzung eines Index 
explain select * from actor where actor_id = 1;
```

```
# Ausgabe ohne Nutzung eines Index
```

