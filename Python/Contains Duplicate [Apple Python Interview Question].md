Question link: https://datalemur.com/questions/python-contains-duplicate


Solution:
```py
def contains_duplicate(input)-> bool:
  list_con = []
  for i in input:
    if i in list_con:
      return True
    list_con.append(i)
    
  return False 
```

