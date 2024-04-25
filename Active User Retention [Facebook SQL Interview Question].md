Solution:
```sql
with cte as(
SELECT *, extract(month from event_date) as mth
FROM user_actions 
)


select mth as month, count(distinct user_id) as monthly_active_users from cte 
where mth = 7 and user_id in (select user_id from cte 
where mth = 6
)
GROUP BY mth
```