
# Y Combinator in Python

```py
def Y(f):
    (lambda x: f(x(x)))(lambda x: f(x(x)))

Y(Y)
```
https://fr.wikipedia.org/wiki/Algorithme_de_Kosaraju
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MjE3MTk1NjcsMTUwNzEyMDYwNCw3Mz
A5OTgxMTZdfQ==
-->