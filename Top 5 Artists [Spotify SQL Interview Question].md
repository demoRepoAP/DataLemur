Question: https://datalemur.com/questions/top-fans-rank

Solution: 
```sql
with cte as (
select a.artist_id, artist_name, s.song_id, day, rank from 
artists as a inner join songs as s on a.artist_id = s.artist_id
inner join global_song_rank as gsr on s.song_id = gsr.song_id
where rank <= 10)

,cte2 as (select artist_name, dense_rank() over (order by cnt desc) as rnk
from
(select artist_name, count(*) as cnt from cte 
group by artist_name ) as x 
)
select artist_name , rnk from cte2
where rnk < 6
```