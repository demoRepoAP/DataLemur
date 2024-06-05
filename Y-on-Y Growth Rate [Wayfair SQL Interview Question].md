Question: https://datalemur.com/questions/yoy-growth-rate

Solution:
```sql
with cte as (
SELECT *, lag(spend,1) over (PARTITION BY product_id order by transaction_date) as prev_year_spend
FROM user_transactions
)
select EXTRACT(year from transaction_date) as year ,product_id,spend as curr_year_spend , prev_year_spend , 
round(100*((spend - prev_year_spend)/prev_year_spend),2) as yoy_rate
from cte
```