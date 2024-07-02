Question link: https://datalemur.com/questions/sql-department-company-salary-comparison

Solution: 
```sql 
with cte as (
select e.department_id, s.payment_date, 
AVG(s.amount)
over (partition by department_id order by payment_date ) as dept_avg,
avg(s.amount) over ()
from employee as e   
inner join salary as s on e.employee_id = s.employee_id
where extract(month from payment_date) = 3
)
select distinct department_id, TO_CHAR(payment_date, 'MM-YYYY'),
case when dept_avg > avg then 'higher' 
when dept_avg < avg then 'lower' else 'Same'
end as comparison
from cte
```