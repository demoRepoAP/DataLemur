Question link: https://datalemur.com/questions/sql-highest-grossing

Solution:

```sql 
with cte as (
SELECT category,product, sum(spend) as total_spend ,
dense_rank() over (partition by category order by sum(spend) desc) as rnk FROM product_spend
where EXTRACT(YEAR FROM transaction_date) = 2022
group by category, product

)
select category, product, total_spend from cte 
where rnk <= 2
``` 
