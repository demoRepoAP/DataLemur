Question link: https://datalemur.com/questions/signup-confirmation-rate

Solution: 
```sql
with cte as (
SELECT e.email_id, user_id, signup_date, signup_action
FROM emails as e   
inner join texts as t on e.email_id = t.email_id
)

SELECT ROUND(CAST(cnt AS DECIMAL) / cnt1, 2) AS result from (select sum(case when signup_action = 'Confirmed' then 1 else 0 end) as cnt,
sum(case when signup_action is not null then 1 else 0 end) as cnt1 from cte)
as x
```