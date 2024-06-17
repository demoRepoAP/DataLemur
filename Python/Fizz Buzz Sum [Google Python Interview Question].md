Question link: https://datalemur.com/questions/python-fizz-buzz-sum

Solution:

```python
def fizz_buzz_sum(target):
  result_list = []
  for i in range(target):
    if i % 3 == 0 or i % 5 == 0:
      result_list.append(i)
  return sum(result_list)
```