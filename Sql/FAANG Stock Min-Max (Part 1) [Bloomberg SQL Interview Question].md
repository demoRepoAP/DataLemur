Question link: https://datalemur.com/questions/sql-bloomberg-stock-min-max-1


Solution 1:
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

Solution 2:
```sql
with high_open as (
select ticker, to_char(date,'Mon-YYYY') as date_month,
rank() over (PARTITION BY ticker order by open desc) as high_rnk,
open from stock_prices  
)
,low_open as (
select ticker, to_char(date,'Mon-YYYY') as date_month,
rank() over (PARTITION BY ticker order by open) as low_rnk, open from stock_prices 
)
select h.ticker, h.date_month as highest_mth, h.open, l.date_month as lowest_mth , l.open
from high_open as h inner join low_open as l on h.ticker = l.ticker
where high_rnk = 1 and low_rnk = 1
```