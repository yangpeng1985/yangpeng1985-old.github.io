```python
def factorial(x):
  if x == 1:
    return 1
  else:
    return x * factorial(x -1)

factorial(3)
```

以上是使用递归计算阶乘的例子；



```python
def sum(x):
  if x == 1:
    return 1
  else:
    return x + sum(x -1)

 sum(10)
```



以上是使用递归计算1到某个正整数所有数字相加值的例子；