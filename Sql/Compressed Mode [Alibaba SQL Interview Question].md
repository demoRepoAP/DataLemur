Question link: https://datalemur.com/questions/alibaba-compressed-mode

Solution:

```sql
ith cte as (
SELECT *, 
rank() over (order by order_occurrences desc) as rnk
FROM items_per_order
)

select item_count from cte 
where rnk = 1
order by item_count
```