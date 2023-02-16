# Part 2: SQL queries / PostgreSQL & pgAdmin

`INNER JOIN` `FULL OUTER JOIN` `LEFT OUTER JOIN` `RIGHT OUTER JOIN` 
<br>
`UNION` 
<br>
`AS`  
<br>
> **JOINs** allows us to combine multiple tables together based on a given **condition** between the two tables.
<br>


<details><summary>DATABASE SCHEMA</summary>
  <p>
    <picture>
      <img alt="Database schema" src="https://user-images.githubusercontent.com/80547490/218577205-91207916-34c1-4f24-91c5-d83b6f9be67a.png">
    </picture>
  </p>
</details>
<br>
<br>

**1. California sales tax laws have changed and we need to alert our customers to this through email. What are the emails of the customers who live in California?**

`INNER JOIN`
<br>

```sql
SELECT * FROM address
INNER JOIN customer 
ON address.address_id = customer.address_id
WHERE district = 'California';
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219332606-97ffcfd5-3502-4f18-87ab-9d9a9ebbdccf.png">
    </picture>
  </p>
</details>
<br>


**2. A customer walks in and is a huge fan of the actor "Nick Wahlberg" and wants to know which movies heis in. Get a list of all the movies "Nick Wahlberg" has been in.**

`INNER JOIN` <br>

```sql
SELECT title AS film_title, (first_name || ' ' || last_name) AS actor 
FROM film_actor
INNER JOIN actor ON film_actor.actor_id = actor.actor_id
INNER JOIN film ON film_actor.film_id = film.film_id
WHERE first_name = 'Nick' AND last_name = 'Wahlberg';
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219339252-ccefbe87-6dd3-43a1-ab15-17b2a5d4dfcc.png">
    </picture>
  </p>
</details>
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

> _I got back empty results, which means the company is in compliance with the new privacy policy._

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219354386-fb2595e1-c50d-4052-8596-90e14a11b8ad.png">
    </picture>
  </p>
</details>
<br>

**There ir another way to solve the previous task:**

`LEFT OUTER JOIN` `WHERE` `IS NULL` <br>

<img src="https://user-images.githubusercontent.com/80547490/219382289-76e46e52-1309-41ba-a742-055f37a91501.png"  width="30%" height="30%">

```sql
SELECT * FROM customer
LEFT OUTER JOIN payment
ON customer.customer_id = payment.customer_id
WHERE payment.payment_id IS null;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219380779-d55438b4-0334-4e40-83eb-09dfac23b6a9.png">
    </picture>
  </p>
</details>
<br>

**4. Select films that are either in just the film table or in both film and inventory tables. Get film_id, title, inventory_id and store_id.**

`LEFT OUTER JOIN` <br>

<img src="https://user-images.githubusercontent.com/80547490/219421825-4bf05d1a-1843-4b63-b139-f6d0db8fb023.png"  width="30%" height="30%">

```sql
SELECT film.film_id, title, inventory_id, store_id FROM film
LEFT JOIN inventory ON film.film_id = inventory.film_id;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219425645-8af90f07-4e01-4968-8cf9-3f0625457763.png">
    </picture>
  </p>
</details>
<br>

**Among the results, find the films that are not in the inventory table.**

`LEFT OUTER JOIN` `WHERE` `IS NULL` <br>

<img src="https://user-images.githubusercontent.com/80547490/219428855-17e038c6-9cd2-4e2b-af52-2696d2251169.png"  width="30%" height="30%">

```sql
SELECT film.film_id, title, inventory_id, store_id FROM film
LEFT JOIN inventory ON film.film_id = inventory.film_id
WHERE inventory.film_id IS null;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219429400-ad898d54-b6be-45f4-b87f-c19003e375fe.png">
    </picture>
  </p>
</details>
<br>
