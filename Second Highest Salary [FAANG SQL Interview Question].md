Question link: https://datalemur.com/questions/sql-second-highest-salary

Solution:

```sql 
with cte as (
select salary, dense_rank() over (order by salary desc) as rnk from employee
)

select salary from cte 
where rnk = 2
```