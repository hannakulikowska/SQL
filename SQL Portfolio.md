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
SELECT DISTINCT (release_year) FROM film;
```

3. How many unique rental rates do we have?

```sql
SELECT COUNT (DISTINCT (rental_rate)) FROM film;
```

