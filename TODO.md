
# Y Combinator in Python

```py
def Y(f):
    (lambda x: f(x(x)))(lambda x: f(x(x)))

Y(Y)
```
https://fr.wikipedia.org/wiki/Algorithme_de_Kos in withad:ad)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEwMjkwMzk2MCwtMTYyMTcxOTU2NywxNT
A3MTIwNjA0LDczMDk5ODExNl19
-->