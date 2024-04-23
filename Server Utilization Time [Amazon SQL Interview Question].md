Solution1: 
```sql
with cte as (
select *, row_number() over (PARTITION BY server_id, session_status order by status_time) as rw from server_utilization
)
,
cte2 AS (
  SELECT server_id, session_status, status_time AS start_time,
    LEAD(status_time) OVER(PARTITION BY server_id, rw ORDER BY status_time) AS stop_time
  FROM cte
  )
  
  SELECT  Sum((CAST(stop_time AS DATE) - CAST(start_time AS DATE))) AS total_uptime_days
  FROM cte2
```
Solution2:
```sql
WITH cte AS (
  SELECT server_id, session_status, status_time AS start_time,
    LEAD(status_time) OVER(PARTITION BY server_id ORDER BY status_time) AS stop_time
  FROM server_utilization
  )

SELECT  Sum((CAST(stop_time AS DATE) - CAST(start_time AS DATE))) AS total_uptime_days
FROM cte
WHERE session_status = 'start'
```