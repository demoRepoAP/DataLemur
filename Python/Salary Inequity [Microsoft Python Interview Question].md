Question link: https://datalemur.com/questions/python-salary-inequity


Solution:
```py
def min_inequity(salaries, n):
	updated_sal = sorted(salaries)
	range_sal = updated_sal[:n]
	return max(range_sal) - min(range_sal)

```