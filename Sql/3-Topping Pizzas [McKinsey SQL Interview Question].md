Solution:
```sql
SELECT CONCAT_WS(',',p1.topping_name, p2.topping_name, p3.topping_name)as pizza,
(p1.ingredient_cost + p2.ingredient_cost + p3.ingredient_cost) as total_cost
FROM pizza_toppings as p1 
cross join pizza_toppings as p2
cross join pizza_toppings as p3  
where p1.topping_name < p2.topping_name and  p2.topping_name < p3.topping_name
ORDER BY total_cost desc, pizza 
```