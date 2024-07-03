Question link: https://datalemur.com/questions/international-call-percentage


```sql
with cte as (
SELECT p.caller_id, pi.country_id as call_cnt, p.receiver_id , po.country_id
as receiver_cnt 
FROM phone_calls as p   
inner join phone_info as pi on p.caller_id = pi.caller_id 
inner join phone_info as po on p.receiver_id = po.caller_id
)
select
round(cast(100*sum(case when call_cnt != receiver_cnt then 1 else 0 end) 
as numeric) 
/ count(*),1) 
from cte
```