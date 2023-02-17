# Part 1: SQL queries / PostgreSQL & pgAdmin

`SELECT` `DISTINCT` `COUNT` 
<br> 
`WHERE` `AND, OR, NOT` 
<br> 
`BETWEEN` `IN` `LIKE` `ILIKE` 
<br>
`MIN, MAX, AVG, SUM` `ROUND` 
<br>
`ORDER BY ASC/DESC` `GROUP BY` `LIMIT` 
<br>
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

**1. What are the first and last names of every customer and their email address?**

```sql
SELECT first_name, last_name, email FROM customer;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219102277-9e9db288-6beb-4dc4-a33d-d02e78827787.png">
    </picture>
  </p>
</details>
<br>

**2. What unique release years do we have inside the film table?**

```sql
SELECT DISTINCT release_year FROM film;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219110869-8a5eff82-6732-4e4a-83c4-78b2310269ec.png">
    </picture>
  </p>
</details>
<br>

**3. How many unique rental rates do we have?**

```sql
SELECT COUNT (DISTINCT rental_rate) FROM film;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219115977-f81fd9ca-3f4c-45ab-bc66-19c1cfaf3af3.png">
    </picture>
  </p>
</details>
<br>

**4. An American visitor isn't familiar with MPAA movie ratings (e.g. PG, PG-13, R, etc.). We want to know the types of ratings we have in our database. What rating do we have available?**

```sql
SELECT DISTINCT rating FROM film;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116076-40ca0219-b9b7-48af-bf2b-61fae4fc1d06.png">
    </picture>
  </p>
</details>
<br>

**5. Find all the rental rates that are higher than a $4, replacement cost is greater than or equal to 19,99 and rating is R. What are film titles?** 

```sql
SELECT title FROM film
WHERE rental_rate > 4 AND replacement_cost >= 19.99 AND rating = 'R';
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116155-4fe47262-6699-46d5-9336-f007a190894b.png">
    </picture>
  </p>
</details>
<br>

**6. How many movies have an R rating or a PG-13 rating?**

```sql
SELECT COUNT(*) FROM film
WHERE rating = 'R' OR rating = 'PG-13';
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116217-17c38fb3-afe4-46ec-a627-b436c72575c6.png">
    </picture>
  </p>
</details>
<br>

**7. Select the films where rating is not equal to R.**

```sql
SELECT * FROM film
WHERE rating != 'R';
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116255-e7ad707b-d0ee-4c42-b4a1-2acb909759eb.png">
    </picture>
  </p>
</details>
<br>

**8. How many customers have the first name Jared?**

```sql
SELECT COUNT(*) FROM customer
WHERE first_name = 'Jared';
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116306-a313149b-5602-439f-95df-5c63fd0dc813.png">
    </picture>
  </p>
</details>
<br>

**9. A customer forgot their wallet at our store. We need to track down their email to inform them. What is email for the customer with the name Nancy Thomas?**

```sql
SELECT email FROM customer
WHERE first_name = 'Nancy' AND last_name = 'Thomas';
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116375-a7f6d6a6-dc9b-4857-a65c-467e749bddf1.png">
    </picture>
  </p>
</details>
<br>

**10. A customer wants to know what the movie "Outlaw Hanky" is about. Could you give them the description for movie?**

```sql
SELECT description FROM film
WHERE title = 'Outlaw Hanky';
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116432-8cf411b6-ca9d-418c-9e5d-433b000953e7.png">
    </picture>
  </p>
</details>
<br>

**11. A customer is late on their movie return and we've mailed them a letter to their address at '259 Ipoh Drive'. We should also call them on the phone to let them know. Can you get the phone number for the customer who lives at '259 Ipoh Drive'?**

```sql
SELECT phone FROM address
WHERE address = '259 Ipoh Drive';
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116486-7e4b592d-1535-47db-ad3a-1023f1bcc788.png">
    </picture>
  </p>
</details>
<br>

**12. Find customers' names who visited our stores. Order them by store ID on descending and first name on ascending.**

```sql
SELECT first_name, last_name FROM customer
ORDER BY store_id DESC, first_name ASC;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116552-986f6e9f-f8d5-4692-abd1-8a052db75895.png">
    </picture>
  </p>
</details>
<br>

**13. We want to reward our first 10 paying customers. What are the customer ids of the first 10 customers who created a payment?**

```sql
SELECT customer_id FROM payment
ORDER BY payment_date ASC
LIMIT 10;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116608-ee93c3a0-6baf-4dd9-9b7d-36f32cf0bda9.png">
    </picture>
  </p>
</details>
<br>

**14. A customer wants to quickly rent a video to watch over their short lunch break. What are the titles of the 5 shortest (in length of runtime) movies?**

```sql
SELECT title, length FROM film
ORDER BY length ASC
LIMIT 5;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116644-8c2a8ae7-adb9-4071-b05f-762a1e027f56.png">
    </picture>
  </p>
</details>
<br>

**15. If the customer can watch any movie that is 50 minutes or less in run time, how many options does this customer have?**

```sql
SELECT COUNT(*) FROM film
WHERE length <= 50;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116688-67529acd-39aa-45d1-8c73-aa753d413bba.png">
    </picture>
  </p>
</details>
<br>

**16. We want to know the actual number of payments that were done not between $8 and $9.**

```sql
SELECT COUNT(*) FROM payment
WHERE amount NOT BETWEEN 8 AND 9;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116744-259a130f-34fe-482b-9bbb-6a17c17f57cd.png">
    </picture>
  </p>
</details>
<br>

**17. What the payments that happened on the first half of February of 2007?**

```sql
SELECT * FROM payment
WHERE payment_date BETWEEN '2007-02-01' AND '2007-02-15';
```
> **Note!** This query is not include 2007-02-15. 
<br>

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116787-2b104604-3c43-43f1-853f-fecaf1ea86aa.png">
    </picture>
  </p>
</details>
<br>

**18. How many payments were not $0.99, $1.98 or $1.99?**

```sql
SELECT COUNT(*) FROM payment
WHERE amount NOT IN (0.99, 1.98, 1.99);
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116842-89aad5df-d635-4b7b-867f-32b73d38ddeb.png">
    </picture>
  </p>
</details>
<br>

**19. Select all the columns from customer table, where the first name are John, Jake or Julie.**

```sql
SELECT * FROM customer
WHERE first_name IN ('John', 'Jake', 'Julie');
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116917-e44395c4-911d-484c-b7c0-1ea41ae2179a.png">
    </picture>
  </p>
</details>
<br>

**20. How many customers actually have a 5 letters name that starts with 'j' and last name that starts with 's'?**

```sql
SELECT COUNT(*) FROM customer
WHERE first_name ILIKE 'j____' AND last_name ILIKE 's%';
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219116995-adcab451-715b-4546-a1db-2c306e9ad592.png">
    </picture>
  </p>
</details>


```sql
SELECT * FROM customer
WHERE first_name ILIKE 'j____' AND last_name ILIKE 's%';
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118078-7080d581-40fd-4117-b7fd-a49fe48972e7.png">
    </picture>
  </p>
</details>
<br>

**21. How many payment transactions were greater than $5.00?**

```sql
SELECT COUNT(*) FROM payment
WHERE amount > 5;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118134-a4973616-90d0-404b-a2f3-73f99561af24.png">
    </picture>
  </p>
</details>
<br>

**22. How many actors have a first name that starts with the letter P?**

```sql
SELECT COUNT(*) FROM actor
WHERE first_name LIKE 'P%'
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118184-48c1b5bc-bbc4-400c-9320-d0be26b8f92e.png">
    </picture>
  </p>
</details>
<br>

**23. How many unique districts are our customers from? Retrieve the list of names for those distincts.**

```sql
SELECT COUNT (DISTINCT district) FROM address;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118229-905d776d-e679-4010-ae17-fc23e884bcf9.png">
    </picture>
  </p>
</details>


```sql
SELECT DISTINCT district FROM address;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118308-12116632-261b-40d3-aac0-f5de4dea4892.png">
    </picture>
  </p>
</details>
<br>

**24. How many films have a rating of R and a replacement cost between $5 and $15?**

```sql
SELECT COUNT(*) FROM film
WHERE rating = 'R' AND replacement_cost BETWEEN 5 AND 15;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118370-e8f48d29-b834-4f8d-830f-d414a5a6dbd1.png">
    </picture>
  </p>
</details>
<br>

**25. How many films have the word Truman somewhere in the title?**

```sql
SELECT COUNT(*) FROM film
WHERE title ILIKE '%truman%';
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118422-8a5af971-9199-4220-87ae-5cdf745997bb.png">
    </picture>
  </p>
</details>
<br>

**26. What the minimum, maximum and average replacement cost was? How much it would cost us to replace all movies?**

```sql
SELECT MIN(replacement_cost), MAX(replacement_cost), ROUND(AVG(replacement_cost),2), SUM(replacement_cost) FROM film;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118474-b0798f52-02b4-48c9-aa00-920e600f8415.png">
    </picture>
  </p>
</details>
<br>

**27. What is the total sum that the every customer spends? Group by customers and by staff members, order by customers and staff.**

```sql
SELECT customer_id, staff_id, SUM(amount) FROM payment
GROUP BY customer_id, staff_id 
ORDER BY customer_id, staff_id;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118510-a83f3e1d-0a1e-42f5-8c80-e9ccc7941f1c.png">
    </picture>
  </p>
</details>
<br>

**28. What is the daily income for the entire period of work?**

```sql
SELECT DATE(payment_date),SUM(amount) FROM payment
GROUP BY DATE(payment_date)
ORDER BY DATE(payment_date);
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118559-1176a037-4944-41a0-8ac1-516bfd5569be.png">
    </picture>
  </p>
</details>
<br>

**29. We have two staff members, which staff ids 1 and 2. We want to give a bonus to the staff member that handled the most payments. How many payments did each staff member handle and who gets the bonus?**

```sql
SELECT staff_id, COUNT(amount) FROM payment
GROUP BY staff_id;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118620-9708b868-646c-48d1-9e9e-b98db1ef4758.png">
    </picture>
  </p>
</details>
<br>

**30. Corporate HQ is conducting a study on the relationship between replacement cost and a movie MPAA rating (e.g. G, PG, R, etc.). What is the average replacement cost per MPAA rating?**

```sql
SELECT rating, ROUND(AVG(replacement_cost),2) FROM film
GROUP BY rating;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118712-9bb7e5c7-baee-4819-baba-44b041499f75.png">
    </picture>
  </p>
</details>
<br>

**31. We are running a promotion to reward our top 5 customers with coupons. What are the customer ids of the top 5 customers by total spend?**

```sql
SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id
ORDER BY SUM(amount) DESC
LIMIT 5;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118774-287fb2d4-1de7-4d2c-aee4-403a924f25fd.png">
    </picture>
  </p>
</details>
<br>

**32. Select customers who spent more than $100.**

```sql
SELECT customer_id, SUM(amount) FROM payment
GROUP BY customer_id
HAVING SUM(amount) > 100;
```

> _HAVING clause allows us to filter after an aggregation has already taken place._

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118844-985fdd04-9049-4397-9245-d9cd649d8d6d.png">
    </picture>
  </p>
</details>
<br>

**33. Select only stores that had more than 300 customers.**

```sql
SELECT store_id, COUNT(customer_id) FROM customer
GROUP BY store_id
HAVING COUNT(customer_id) > 300;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118927-de0e8764-abf8-4732-b9a8-006997b483a9.png">
    </picture>
  </p>
</details>
<br>

**34. We are launching a platinum service for our most loyal customers. We will assign platinum status to customers that have had 40 or more transaction payments. What customer ids are eligible for platinum status?**

```sql
SELECT customer_id, COUNT(*) FROM payment
GROUP BY customer_id
HAVING COUNT(*) >= 40;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219118987-3479d620-8d55-4cae-8936-85adc018e7f5.png">
    </picture>
  </p>
</details>
<br>

**35. What are the customer ids of customers who have spent more than $100 in payment transactions with our staff_id member 2?**

```sql
SELECT customer_id, SUM(amount) FROM payment
WHERE staff_id = 2
GROUP BY customer_id
HAVING SUM(amount) > 100;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219119045-f66ca857-03b6-4069-bcc6-7c8104f8f76d.png">
    </picture>
  </p>
</details>
<br>

**36. Return the customer ids of customers who have spent at least $110 with the staff member who has an ID of 2.**

```sql
SELECT customer_id, SUM(amount) FROM payment
WHERE staff_id = 2
GROUP BY customer_id
HAVING SUM(amount) >= 110;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219119103-9218ae0f-53f8-4094-9219-0b783f7cbccf.png">
    </picture>
  </p>
</details>
<br>

**37. What customer has the highest customer ID number whose name starts with an 'E' and has an adress ID lower than 500?**

```sql
SELECT first_name, last_name FROM customer
WHERE first_name LIKE 'E%' AND address_id < 500
ORDER BY customer_id DESC
LIMIT 1;
```

<details><summary>Screenshot</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/219119167-d5901548-cebe-4486-8b1a-c71cfaa60d6f.png">
    </picture>
  </p>
</details>
