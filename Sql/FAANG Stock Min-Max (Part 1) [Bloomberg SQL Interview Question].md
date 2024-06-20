Question link: https://datalemur.com/questions/sql-bloomberg-stock-min-max-1


Solution:
```sql
with cte as (
SELECT ticker,
to_char(date,'Mon-YYYY') as date_month,open,
rank() over (PARTITION BY ticker order by open desc) as maxi_high,
rank() over (PARTITION BY ticker order by open ) as maxi_low
FROM stock_prices 
)

select ticker, 
max(case when maxi_high = 1 then date_month end) as highest_mth ,
max(open) as higest_open,
max(case when maxi_low = 1 then date_month end) as lowest_mth,
min(open) as lowest_open from cte
group by ticker
```
