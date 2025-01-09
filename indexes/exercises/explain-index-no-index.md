# Explain index, no index 

```
create table actorneu as select * from actor
```

```
# Ausgabe mit Nutzung eines Index 
explain select * from actor where actor_id = 1;
explain sleect * from actor;
```

```
# Ausgabe ohne Nutzung eines Index
explain select * from actorneu where actor_id = 1;
```

