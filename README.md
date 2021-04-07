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
- Kata: https://www.codewars.com/kata/5994dafcbddc2f116d000024/train/sql
```
SELECT player_name, games, 
    CAST( ROUND( CAST(hits AS numeric) / at_bats  ,3)  as varchar)
    AS batting_average
FROM yankees
WHERE at_bats >= 100
ORDER BY batting_average DESC;
```
Alternatives that I liked done by other users
```
select player_name,
       games,
       round(hits::numeric / at_bats, 3)::text as batting_average
from yankees
where at_bats > 100
order by 3 desc

SELECT player_name, games, to_char(hits/at_bats::real, 'FM0D000') as batting_average
FROM yankees
WHERE at_bats >= 100
ORDER BY batting_average DESC
```
