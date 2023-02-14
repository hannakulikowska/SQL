# My SQL portfolio

</details>
<details><summary>Database scheme PostgreSQL</summary>
  <p>
    <picture>
      <img alt="Database scheme" src="https://user-images.githubusercontent.com/80547490/218577205-91207916-34c1-4f24-91c5-d83b6f9be67a.png">
    </picture>
  </p>
</details>
<br>

1. What are the first and last names of every customer and their email address?

```sql
SELECT first_name, last_name, email FROM customer;
```

2. What UNIQUE release years do we have inside the film table?

```sql
SELECT DISTINCT release_year FROM film;
```

3. How many unique rental rates do we have?

```sql
SELECT COUNT (DISTINCT rental_rate) FROM film;
```

4. An American visitor isn't familiar with MPAA movie ratings (e.g. PG, PG-13, R, etc.). We want to know the types of ratings we have in our database. What rating do we have available?

```sql
SELECT DISTINCT rating FROM film;
```

5. Find all the rental rates that are higher than a $4, replacement cost is greater than or equal to 19,99 and rating is R. What are film titles? 

```sql
SELECT title FROM film
WHERE rental_rate > 4 AND replacement_cost >= 19,99 AND rating = 'R';
```

6. How many movies have an R rating or a PG-13 rating?

```sql
SELECT COUNT(*) FROM film
WHERE rating = 'R' OR rating = 'PG-13';
```

7. Select the films where rating is not equal to R.

```sql
SELECT * FROM film
WHERE rating != 'R';
```

8. How many customers have the first name Jared?

```sql
SELECT COUNT(*) FROM customer
WHERE first_name = 'Jared';
```

9. A customer forgot their wallet at our store. We need to track down their email to inform them. What is email for the customer with the name Nancy Thomas?

```sql
SELECT email FROM customer
WHERE first_name = 'Nancy' AND last_name = 'Thomas';
```

</details>
<details><summary>Screen</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/218683805-fe72cc5d-cfae-4a3c-981a-a9fb63ccc82c.png">
    </picture>
  </p>
</details>

10. A customer wants to know what the movie "Outlaw Hanky" is about. Could you give them the description for this movie?

```sql
SELECT description FROM film
WHERE title = 'Outlaw Hanky';
```

11. A customer is late on their movie return and we've mailed them a letter to their address at '259 Ipoh Drive'. We should also call them on the phone to let them know. Can you get the phone number for the customer who lives at '259 Ipoh Drive'?

```sql
SELECT phone FROM address
WHERE address = '259 Ipoh Drive';
```

12. Find customers' names who visited our stores. Order them by store ID on descending and first name on ascending.

```sql
SELECT first_name, last_name FROM customer
ORDER BY store DESC, first_name ASC;
```

13. We want to reward our first 10 paying customers. What are the customer ids of the first 10 customers who created a payment?

```sql
SELECT customer_id FROM payment
ORDER BY payment_date ASC
LIMIT 10;
```

14. A customer wants to quickly rent a video to watch over their short lunch break. What are the titles of the 5 shortest (in length of runtime) movies?

```sql
SELECT title, length FROM film
ORDER BY length ASC
LIMIT 5;
```

15. If the customer can watch any movie that is 50 minutes or less in run time, how many options does this customer have?

```sql
SELECT COUNT(*) FROM film
WHERE length <= 50;
```

16. We want to know the actual number of payments that were done not between $8 and $9.

```sql
SELECT COUNT(*) FROM payment
WHERE amount NOT BETWEEN 8 AND 9;
```

</details>
<details><summary>Screen</summary>
  <p>
    <picture>
      <img alt="screen" src="https://user-images.githubusercontent.com/80547490/218711760-070bc26a-b9cb-44de-a5c7-860f2864a73a.png">
    </picture>
  </p>
</details>

17. What the payments that happened on the first half of February of 2007?

```sql
SELECT * FROM payment
WHERE payment_date BETWEEN '2007-02-01 AND '2007-02-15';
```
> **Note!** Thise query is not include 2007-02-15. 
<br>

18. How many payments were not $0.99, $1.98 or $1.99?

```sql
SELECT COUNT(*) FROM payment
WHERE amount NOT IN (0.99, 1.98, 1.99);
```

19. Select all the columns from customer table, where the first name are John, Jake or Julie.

```sql
SELECT * FROM customer
WHERE first_name IN ('John', 'Jake', 'Julie');
```

20. 
