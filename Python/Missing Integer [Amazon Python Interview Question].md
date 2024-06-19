Question link: https://datalemur.com/questions/python-missing-integer

Solution:
```py
def missing_int(input: list[int])-> int:
     n = len(input)
     
     n_sum = n*(n+1)//2
     actual_sum = sum(input)
     diff = n_sum - actual_sum
     return diff
```