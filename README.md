# SQL Notes


- Select the month from a date column:
```
SELECT 
  EXTRACT(MONTH FROM payment_date) AS month
FROM payment;
```
