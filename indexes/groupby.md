# Index on GroupBy 

![image](https://github.com/user-attachments/assets/e45c829f-8456-47bc-8f33-05cce6e05b88)


![image](https://github.com/user-attachments/assets/0d03e530-7e2e-4bcb-8167-ae5600fe3287)

```
Variante 1:
explain SELECT last_name, COUNT(*) AS 'count'
  FROM actor
  WHERE first_name LIKE 'S%'
  GROUP BY last_name

Variante 2:
explain SELECT first_name, COUNT(*) AS 'count'
  FROM actor
  WHERE last_name LIKE 'S%'
  GROUP BY first_name
```
