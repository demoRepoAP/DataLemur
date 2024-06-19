Question link: https://datalemur.com/questions/sql-swapped-food-delivery


Solution: 
```sql
with cte as(
SELECT order_id, item, row_number() over (order by order_id) as rw,
case when row_number() over (order by order_id) % 2 = 0 then lag(item,1) over (order by order_id)
when row_number() over (order by order_id) % 2 = 1 then lead(item,1,item) over (order by order_id)
end as new_item
FROM orders 
)

select order_id, new_item as item from cte
```