
# Y Combinator in Python

```py
def Y(f):
    (lambda x: f(x(x)))(lambda x: f(x(x)))

Y(Y)
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUwNzEyMDYwNCw3MzA5OTgxMTZdfQ==
-->