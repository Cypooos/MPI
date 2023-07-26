
# La machine de Cythan

La machine de Cythan constite en un tableau d'entier positifs $T[n]$ indexé par des entiers positifs.
A chaque itération de la machine, les deux opérations suivantes sont réalisées :
1. $T[0] \larr u[0]+2$
2. $T[T[T[0]-2]] \larr T[T[T[0]-1]]$

Si l'état de la machine ne change pas après une itération, alors elle s’arrête.
Pour comprendre ces deux opérations, il faut voir $T[0]$ comme l'*instruction pointer* de la machine, incrémenté à chaque itération, et voir la deuxième comme l'opération `mov T[T[0]-2] [T[T[0]-1]]` .

Enfaîte, ces deux opérations sont équivalente à :
- Take the value pointed by the _instruction pointer_ (cell at index 0), and the value behind
-  Execute a `mov` on the cells at index value 1 and value 2
-   If cell 0 didn't changed, add 2 to cell 0
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTE5NTk3NDU5XX0=
-->