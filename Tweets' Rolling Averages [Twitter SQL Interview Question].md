Question: https://datalemur.com/questions/rolling-average-tweets

Solution: 
```sql
SELECT user_id, tweet_date, round(avg(tweet_count) over 
(PARTITION BY user_id order by tweet_date rows BETWEEN 2 preceding and current row),2)
FROM tweets
order by user_id
```