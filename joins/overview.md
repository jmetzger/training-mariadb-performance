# Overview Joins

```

 * combines rows from two or more tables
 * based on a related column between them.


```

## MariaDB (Inner) Join 


![image](https://github.com/user-attachments/assets/b0c54d02-95b6-4593-bd5d-d290d42a5729)


## MariaDB (Inner) Join (explained) 

```
  * Inner Join and Join are the same
  * Returns records that have matching values in both tables
  * Inner Join, Cross Join and Join 
    * are the same in MySQL
 ```

 
## MariaDB Left Join

![image](https://github.com/user-attachments/assets/c486eb59-bf64-44e7-abce-7ac1c4e18731)



## MySQL Left (outer) Join (explained) ==== 

  * Return all records from the left table
  * _AND_ the matched records from the right table
  * The result is NULL on the right side
    * if there are no matched columns on the right 
  * Left Join and Left Outer Join are the same

## MySQL Right Join


![image](https://github.com/user-attachments/assets/69935a67-78fb-44d2-86ea-cdefe3060734)

## MySQL Right Join (explained)

  * Return all records from the right table
    * _AND_ the matched records from the left table
  * Right Join and Right Outer Join are the same

## MySQL Straight Join 

  * MySQL (inner) Join and Straight Join are the same
  * **Difference:**
    * The left column is always read first
  * **Downside:**
    * Bad optimization through mysql (query optimizer) 
  * **Recommendation:**
    * Avoid straight join if possible 
    * use join instead 

## Type of Joins

  * [inner] join
    * **inner join** and **join** are the same  
  * left [outer] join 
  * right [outer] join
  * full [outer] join
  * straight join < equals > join
  * cross join = join (in mysql)
  * natural join <= equals => join (but syntax is different)

## In Detail: [INNER] JOIN 

  * Return rows when there 
    * is a match in both tables 
  * Example 

```
SELECT actor.first_name, actor.last_name, film.title 
FROM film_actor 
INNER JOIN actor ON film_actor.actor_id = actor.actor_id 
INNER JOIN film ON film_actor.film_id = film.film_id;
```

## In Detail: Joining without JOIN - Keyword

  * Explanation: Will have the same query execution plan as [INNER] JOIN

```
SELECT actor.first_name, actor.last_name, film.title 
FROM film_actor,actor,film 
where film_actor.actor_id = actor.actor_id 
and film_actor.film_id = film.film_id;
```

## In Detail: Left Join

  * Return all rows from the left side
    * even if there is not result on the right side
  * Example

```
SELECT 
	c.customer_id, 
    c.first_name, 
    c.last_name,
    a.actor_id,
    a.first_name,
    a.last_name
FROM customer c
LEFT JOIN actor a 
ON c.last_name = a.last_name
ORDER BY c.last_name;
```

## In Detail: Right Join

  * Return all rows from the right side
    * even if there are no results on the left side
  * Example 

```
SELECT 
    c.customer_id, 
    c.first_name, 
    c.last_name,
    a.actor_id,
    a.first_name,
    a.last_name
FROM customer c
RIGHT JOIN actor a 
ON c.last_name = a.last_name
ORDER BY a.last_name;
```

## In Detail: Having

  * Simple: WHERE for GroupBy (because where does not work here)
  * Example

```
SELECT last_name, COUNT(*) 
FROM sakila.actor
GROUP BY last_name
HAVING count(last_name) > 2
```
 
## Internal (type of joins)  - NLJ 

  * NLJ - (Nested Loop Join)

```
for each row in t1 matching range {
  for each row in t2 matching reference key {
    for each row in t3 {
      if row satisfies join conditions, send to client
    }
  }
}
```

## Internal (type of joins) - BNL 
 
  * BNL - (Block Nested Loop) 
    * in explain: -> using join buffer 
    * columns of interest to a join are stored in join buffer
      * --> not whole rows.
    * join_buffer_size system variable 
      * -> determines the size of each join buffer used to process a query. 
  * https://dev.mysql.com/doc/refman/5.7/en/nested-loop-joins.html

## BNL - Who can I see, if it is used ?

  * Can be seen in explain 

![image](https://github.com/user-attachments/assets/06380456-a4e2-4213-9b71-b2621bfdb91c)

  
```
  * explain select * from t1, t2 where t1.col < 10 and t2.col < 'bar';
```


