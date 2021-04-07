# SQL Notes


- Kata: https://www.codewars.com/kata/5816a3ecf54413a113000074/train/sql
```
SELECT 
  EXTRACT(MONTH FROM payment_date) AS month,
  COUNT(amount) AS total_count,
  SUM(amount) AS total_amount,
  SUM(CASE WHEN staff_id = 1 THEN 1 ELSE 0 END) as mike_count,
  SUM(CASE WHEN staff_id = 1 THEN amount ELSE 0 END) as mike_amount,
  SUM(CASE WHEN staff_id = 2 THEN 1 ELSE 0 END) as jon_count,
  SUM(CASE WHEN staff_id = 2 THEN amount ELSE 0 END) as jon_amount
FROM payment
WHERE staff_id = 1 OR staff_id = 2
GROUP BY month
ORDER BY month;
```
Alternative that I liked done by other user
```
SELECT
  EXTRACT(MONTH FROM payment_date)        AS month,
  COUNT(*)                                AS total_count,
  SUM(amount)                             AS total_amount,
  COUNT(*)    FILTER (WHERE staff_id = 1) AS mike_count,
  SUM(amount) FILTER (WHERE staff_id = 1) AS mike_amount,
  COUNT(*)    FILTER (WHERE staff_id = 2) AS jon_count,
  SUM(amount) FILTER (WHERE staff_id = 2) AS jon_amount
FROM payment
GROUP BY month
ORDER BY month;
```
