Question: https://datalemur.com/questions/supercloud-customer

Solution: 
```sql
with cte as (
SELECT customer_id, p.*
FROM products as p
inner join customer_contracts as cc on p.product_id = cc.product_id
)
select customer_id from cte
GROUP BY customer_id 
having count(distinct product_category) > 2
```