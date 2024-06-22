Question: https://datalemur.com/questions/python-max-profit-trading-stocks


Solution:
```py
def max_subarray_sum(prices):
	min_price = min(prices)
	max_price = max(prices)
	
	while prices.index(max_price) > prices.index(min_prices):
	  prices.remove(max_price)
	  min_price = min(prices)
	  max_price = max(prices)
	return (max_price - min_price)

```