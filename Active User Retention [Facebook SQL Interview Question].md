Solution:
```sql
SELECT date_part('month', event_date),
count(DISTINCT user_id) monthly_active_users
FROM  user_actions
where user_id in (
select user_id from user_actions
where date_part('month',event_date) = 6)
and 
date_part('month',event_date) = 7
GROUP BY 1
```