Question link: https://datalemur.com/questions/python-factorial-trailing-zeroes

Solution:
```py
def trailing_zeroes(n):
    if n < 0:
        return None  # Trailing zeros are not defined for negative numbers
    trailing_zeros = 0
    while n >= 5:
        n //= 5
        trailing_zeros += n
    return trailing_zeros      
         
```