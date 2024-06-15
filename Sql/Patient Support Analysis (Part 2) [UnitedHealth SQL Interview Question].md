Questin link: https://datalemur.com/questions/uncategorized-calls-percentage

Solution:
```sql 
with cte as (
SELECT 
SUM(case when call_category = 'n/a' or call_category is null
then 1 else 0 end) as cnt, count(*) as total_cnt
FROM callers
)

select round(100*cast(cnt as numeric)/total_cnt,1) as uncategorised_call_pct from cte
```


