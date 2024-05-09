Question: https://datalemur.com/questions/updated-status

Solution:
```sql
SELECT COALESCE(a.user_id, dp.user_id) as user_id,
CASE 
WHEN paid is NULL THEN 'CHURN' 
WHEN paid is not NULL AND status in ('NEW','EXISTING','RESURRECT') THEN 'EXISTING'
WHEN paid is not NULL AND status = 'CHURN' THEN 'RESURRECT'
WHEN paid is not NULL AND status is NULL  THEN 'NEW'
end as new_status
FROM advertiser a
FULL OUTER JOIN daily_pay dp on dp.user_id = a.user_id
ORDER BY user_id
```