Question link: https://datalemur.com/questions/python-intersection-of-two-lists


Solution 1:
```py
def intersection(a, b):
    comm_list = []
    for i in a:
        for j in b:
            if i == j:
                comm_list.append(i)
    return comm_list

```

Solution 2:
```py
def intersection(a,b):
  return list(set(a)& set(b))
```