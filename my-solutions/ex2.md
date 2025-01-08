## Basic Level

```sql
-- 1. List all customers' first names in uppercase and last names in lowercase.
SELECT UPPER(first_name),
       LOWER(last_name)
FROM customer


-- 2. Display the first 3 characters of each customer's email address alongside their full name.
SELECT SUBSTRING(email for 3),
       first_name || ' ' ||
       last_name as full_name
FROM customer

-- 3. Show the length of each customer's full name (first name + last name).
SELECT first_name || last_name as full_name,
       LENGTH(first_name || last_name)
FROM customer

-- 4. Extract the domain name from each customer's email address.
SELECT emaiL,
       LOWER(LEFT (email, position('@' in email) - 1)) as domain
FROM customer

-- 5. Concatenate each customer's first name and last name with a space in between.
SELECT first_name || ' ' ||
       last_name
FROM customer

```

## Intermediate Level

```sql
-- 6. Create a username for each customer by concatenating the first 3 letters of their 
-- first name with the last 3 letters of their last name, all in lowercase.
SELECT first_name || ' ' || last_name                      as full_name,
       LOWER(LEFT (first_name, 3) || RIGHT (last_name, 3)) as username
FROM customer

-- 7. Display customer names in the format "LASTNAME, F." where F is the first character of the first name.
SELECT first_name || ' ' || last_name as full_name,
       last_name || ', ' || LEFT(first_name, 1)
FROM customer

-- 8. List customers whose first name or last name contains more than 10 characters.
SELECT first_name || ' ' || last_name as full_name
FROM customer
WHERE LENGTH(first_name) >= 10
   or LENGTH(last_name) >= 10

-- 9. Extract the part of the email address before the '@' symbol for each customer.
SELECT
    LEFT (email, position ('@' in email) -1)
FROM customer

-- 10. Find the position of the dot (.) in customer email addresses and display it alongside the full email.
SELECT POSITION('.' in email),
       email
FROM customer


```

## Advanced Level

```sql
-- 11. Create an anonymized version of customer emails in the format "F***L@domain.com", 
-- where F is the first character of the first name and L is the first character of the last name.
SELECT
    LEFT (first_name, 1) || '***' ||
    LEFT (last_name, 1 ) ||
    SUBSTRING (email, position ('@' in email))
FROM customer
```

```sql
-- 12. Generate a simple customer ID by concatenating:
--  > The first 2 characters of their first name (uppercase)
--  > The last 2 characters of their last name (lowercase)
--  > The length of their email address
SELECT UPPER(LEFT (first_name, 2)) ||
       LOWER(RIGHT (last_name, 2)) ||
       LENGTH(email) as customer_id,
       email
FROM customer
```

```sql
-- 13. Display customer names where the middle character(s) are replaced with asterisks. 
-- For odd-length names, replace the middle character. For even-length names, replace the two middle characters.
SELECT
    LENGTH(first_name),
    first_name,
    CASE
        -- For odd-length names
        WHEN LENGTH(first_name) % 2 = 1 THEN
            LEFT(first_name, (LENGTH(first_name) - 1) / 2) ||
            '*' ||
            RIGHT(first_name, (LENGTH(first_name) - 1) / 2)
 
        -- For even-length names
        ELSE
          LEFT(first_name, (LENGTH(first_name) / 2) - 1) ||
          '**' ||
         RIGHT(first_name, LENGTH(first_name) / 2 - 1)
END AS replaced_name
FROM customer;
```

