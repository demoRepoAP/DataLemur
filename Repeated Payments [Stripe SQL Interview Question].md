Question link: https://datalemur.com/questions/repeated-payments

Solution:
```sql
with cte as (
SELECT *, count(merchant_id) over 
(PARTITION BY merchant_id,credit_card_id, amount ORDER BY transaction_timestamp), 
lag(transaction_timestamp,1)
OVER(PARTITION BY merchant_id,credit_card_id,amount ORDER BY transaction_timestamp) as prev_date
FROM transactions
)

select count(1) as payment_count from (select transaction_id, 
ROUND(EXTRACT(epoch FROM AGE(transaction_timestamp, prev_date)) / 60,0) 
AS 
diff_in_minutes
from cte
) as x 
where diff_in_minutes <= 10
```