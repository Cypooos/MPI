
# Y Combinator in Python

```py
def Y(f):
    (lambda x: f(x(x)))(lambda x: f(x(x)))

Y(Y)
```

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzMwOTk4MTE2XX0=
-->
