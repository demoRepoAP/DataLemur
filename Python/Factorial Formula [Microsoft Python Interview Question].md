Question link: https://datalemur.com/questions/python-factorial-formula

Solution:

```python
def factorial(n):
  if n <= 0 :
    return 1
  else:
      return n* factorial(n-1)
      
```

