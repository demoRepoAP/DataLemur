Question: https://datalemur.com/questions/odd-even-measurements

Solution:

```sql 
with cte as (
select measurement_id, measurement_value, cast(measurement_time as date),
row_number() over (PARTITION BY CAST(measurement_time AS date) ORDER BY measurement_time) as rw
from measurements

)
select
measurement_time, 
sum(case when rw%2 = 0 then measurement_value else 0 end) as even_sum,
sum(case when rw%2 != 0 then measurement_value else 0 end) as odd_sum
from cte 
group by measurement_time
```