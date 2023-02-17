# Part 2: SQL queries / PostgreSQL & pgAdmin

`INNER JOIN` `FULL OUTER JOIN` `LEFT OUTER JOIN` `RIGHT OUTER JOIN` 
<br>
`UNION` 
<br>
`AS`  
<br>
> **JOIN** allows us to combine multiple tables together based on a given **condition** between the two tables. <p>
> **UNION** is used to combine the results of two or more SELECT statements. <br>
>   - Every SELECT statement within UNION must have the same number of columns.
>   - The columns must have similar data types.
>   - The columns in every SELECT statement must be in the same order.
<br>


<details><summary>Click here to see the DATABASE SCHEMA</summary>
  <p>
    <picture>
      <img alt="Database schema" src="https://user-images.githubusercontent.com/80547490/218577205-91207916-34c1-4f24-91c5-d83b6f9be67a.png">
    </picture>
  </p>
</details>
<br>
<br>

**1. California sales tax laws have changed and we need to alert our customers to this through email. What are the emails of the customers who live in California?**

`INNER JOIN` `WHERE`
<br>

<img src="https://user-images.githubusercontent.com/80547490/219630786-1976f4dd-789e-4933-b1df-91be91da8b67.png" width="30%" height="30%">

```sql
SELECT * FROM address
INNER JOIN customer 
ON address.address_id = customer.address_id
WHERE district = 'California';
```

<img src="https://user-images.githubusercontent.com/80547490/219613357-c53d93c2-64d4-4b1e-8c4f-5fdaab1b1f85.png">
<br>

**2. A customer walks in and is a huge fan of the actor "Nick Wahlberg" and wants to know which movies heis in. Get a list of all the movies "Nick Wahlberg" has been in.**

`INNER JOIN` `WHERE` <br>

<img src="https://user-images.githubusercontent.com/80547490/219635641-7d5a6f14-87f2-4400-b49b-a0f8a2d0a028.png" width="30%" height="30%">

```sql
SELECT title AS film_title, (first_name || ' ' || last_name) AS actor 
FROM film_actor
INNER JOIN actor ON film_actor.actor_id = actor.actor_id
INNER JOIN film ON film_actor.film_id = film.film_id
WHERE first_name = 'Nick' AND last_name = 'Wahlberg';
```

<img src="https://user-images.githubusercontent.com/80547490/219613570-5410fe3e-da1f-4866-ae49-50c4b6725026.png" width="20%" height="20%">
<br>

**3. Some new privacy rules have been implemented and we want to make sure that we don't have any payment information that's not attached to customer or that we don't have some customer information that isn't attached to any payments. Essentially, we want to make sure that all the payments we have is associated with a current customer and all the customers we have are associated with some historical payment.**

`FULL OUTER JOIN` `WHERE` `IS NULL` <br>

<img src="https://user-images.githubusercontent.com/80547490/219365717-8b79d770-8c79-465e-80e8-82a3c3880072.png"  width="30%" height="30%">

```sql
SELECT * FROM customer
FULL OUTER JOIN payment
ON customer.customer_id = payment.customer_id
WHERE customer.customer_id IS null
OR payment.payment_id IS null;
```

![3 1](https://user-images.githubusercontent.com/80547490/219613678-36b43e76-952f-4773-8b5e-ede6c6b81622.png)
> _I got back empty results, which means the company is in compliance with the new privacy policy._
<br>
    
**There are other ways to solve the previous task:**

`LEFT OUTER JOIN` `WHERE` `IS NULL` <br>

<img src="https://user-images.githubusercontent.com/80547490/219382289-76e46e52-1309-41ba-a742-055f37a91501.png"  width="30%" height="30%">

```sql
SELECT * FROM customer
LEFT OUTER JOIN payment
ON customer.customer_id = payment.customer_id
WHERE payment.payment_id IS null;
```

![3 2](https://user-images.githubusercontent.com/80547490/219613753-64bc8745-6fe2-4518-9c0e-3b3b57fce313.png)
<br>

**OR**

`RIGHT OUTER JOIN` `WHERE` `IS NULL` <br>

<img src="https://user-images.githubusercontent.com/80547490/219620870-6fd8b03d-8dec-4932-b3c8-9a86b20332ee.png"  width="30%" height="30%">

```sql
SELECT * FROM customer
RIGHT OUTER JOIN payment
ON customer.customer_id = payment.customer_id
WHERE customer.customer_id IS null;
```

![3 3](https://user-images.githubusercontent.com/80547490/219619828-d330ff0c-b1c4-4106-848e-d119cd182a44.png)
<br>

**4. Select films that are either in just the film table or in both film and inventory tables. Get film_id, title, inventory_id and store_id.**

`LEFT OUTER JOIN` <br>

<img src="https://user-images.githubusercontent.com/80547490/219421825-4bf05d1a-1843-4b63-b139-f6d0db8fb023.png" width="30%" height="30%">

```sql
SELECT film.film_id, title, inventory_id, store_id FROM film
LEFT JOIN inventory ON film.film_id = inventory.film_id;
```

<img src="https://user-images.githubusercontent.com/80547490/219613852-74c671ae-e2fd-4eab-992e-5bcf0f8d5f2c.png" width="30%" height="30%">
<br>

**Among the results, find the films that are not in the inventory table.**

`LEFT OUTER JOIN` `WHERE` `IS NULL` <br>

<img src="https://user-images.githubusercontent.com/80547490/219428855-17e038c6-9cd2-4e2b-af52-2696d2251169.png"  width="30%" height="30%">

```sql
SELECT film.film_id, title, inventory_id, store_id FROM film
LEFT JOIN inventory ON film.film_id = inventory.film_id
WHERE inventory.film_id IS null;
```

<img src="https://user-images.githubusercontent.com/80547490/219614004-d883e49a-2995-49a1-a326-5d3c65d3c0cd.png" width="30%" height="30%">
<br>
