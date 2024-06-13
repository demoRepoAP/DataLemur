Question: https://datalemur.com/questions/card-launch-success

Solution: 
```sql
with cte as (
SELECT *, row_number() over (PARTITION BY card_name order by issue_year, issue_month) as rw
FROM monthly_cards_issued
)
select card_name , issued_amount from cte 
where rw = 1
order by issued_amount desc
```