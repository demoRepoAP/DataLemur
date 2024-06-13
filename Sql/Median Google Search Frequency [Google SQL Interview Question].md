Question: https://datalemur.com/questions/median-search-freq

Solution:
```sql
with cte as (
SELECT *,SUM(num_users) OVER(ORDER BY searches) as running_sum 
, sum(num_users) over () usersum
FROM search_frequency 
)

select round(avg(searches),1) from  cte  
where running_sum in (floor((usersum+1)*1.0/2), ceiling((usersum+1)*1.0/2)) 
```


