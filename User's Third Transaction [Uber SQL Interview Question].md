Question: https://datalemur.com/questions/sql-third-transaction


Solution:

```sql
with cte as 
(SELECT *, row_number() over (PARTITION BY user_id order by transaction_date) as rw
FROM transactions
)

select user_id, spend, transaction_date from cte 
where rw = 3
```