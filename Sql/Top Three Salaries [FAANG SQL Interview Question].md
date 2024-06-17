Question link: https://datalemur.com/questions/sql-top-three-salaries


Solution: 
```sql
with cte as (
select department_name, name, salary, dense_rank() over (PARTITION BY e.department_id order by salary desc) as rnk from employee as e  
join department as d on e.department_id = d.department_id 
order by d.department_id,  e.salary desc, e.name
)
select department_name, name, salary from cte 
where rnk <= 3
```