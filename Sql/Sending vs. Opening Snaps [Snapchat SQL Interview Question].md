Question: https://datalemur.com/questions/time-spent-snaps

Solution:
```sql 
with cte as (
SELECT age_bucket, 
sum(case when activity_type = 'open' then time_spent end) as open,
sum(case when activity_type = 'send' then time_spent end) as send,
sum(time_spent) as total
FROM activities as a inner join age_breakdown as ag 
on a.user_id = ag.user_id and a.activity_type !='chat'
group by age_bucket
)
select age_bucket, round(100*(send/total),2) as send_prec, round(100*(open/total),2) as open_prec from cte 
```
