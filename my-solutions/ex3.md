## Basic Exercises

```sql
-- 1.  Using the customer table, extract the year from the create_date column for all customers.
SELECT extract(year from create_date)
FROM customer;

-- 2. From the rental table, extract the month and year from the rental_date column.
SELECT to_char(rental_date, 'Month') as month, 
extract(year from rental_date) as year
FROM rental;

-- 3. Use TO_CHAR to format the last_update timestamp in the customer table as "Month DD, YYYY".
SELECT to_char(last_update, 'Month DD, YYYY')
FROM rental;

-- 4. Calculate the age of each customer as of today using the create_date from the customer table.
SELECT customer_id,
       (extract(year from current_date) - extract(year from create_date)) as age
FROM customer;

-- 5. Find the day of the week (as a string) with the most rentals from the rental table.
SELECT to_char(rental_date, 'Day') as day_of_the_week,
       count(*)                    as total_rents_per_day
FROM rental
group by to_char(rental_date, 'Day')
order by total_rents_per_day desc limit 1;

```

## Intermediate Exercises

## Advanced Exercises