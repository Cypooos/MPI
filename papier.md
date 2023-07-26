
# La machine de Cythan

La machine de Cythan constite en un tableau d'entier positifs $T[n]$ indexé par des entiers positifs.
A chaque itération de la machine, les deux opérations suivantes sont réalisées :
1. $T[0] \larr u[0]+2$
2. $T[T[T[0]-1]] \larr T[T[T[0]-2]]$

Si l'état de la machine ne change pas après une itération, alors elle s’arrête.
Pour comprendre ces deux opérations, il faut voir $T[0]$ comme le programe co
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg5Mzg4Mjg4MF19
-->