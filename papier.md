
# La machine de Cythan

La machine de Cythan constite en un tableau d'entier positifs $T[n]$ indexé par des entiers positifs.
A chaque itération de la machine, les deux opérations suivantes sont réalisées :
1. $T[0] \larr T[0]+2$
2. $T[T[T[0]-2]] \larr T[T[T[0]-1]]$

Si l'état de la machine ne change pas après une itération, alors elle s’arrête.
Pour comprendre ces deux opérations, il faut voir $T[0]$ comme l'*instruction pointer* de la machine, incrémenté à chaque itération, et voir la deuxième comme l'opération `mov T[T[0]-2] [T[T[0]-1]]` .

Enfaîte, ces deux opérations sont équivalentes aux instructions :
- $(v_1,v_2) = (T[IP],T[IP+1])$ avec $IP = T[0]$, l'*Instruction pointeur*
- $T[v_1] \larr T[v_2]$
- Si $T[0]$ n'a pas été modifié, alors $T[0] \larr T[0] + 2$

### JUMP

On considère le code 
| position |  0  | ... | $p$ | $p+1$ | $p+2$ |
|----------|-----|-----|-----|-------|-------|
| **code** | $p$ | ... |  0  | $p+2$ | $k$ |

Si l'on effecture l'itération, l'on fera $T[T[T[0]+2-2]] = T[T[p]]=T[0] \larr T[T[T[0]+2-1]] = T[T[p+1]]=T[p+2]=k$, soit l'opération $T[0] \larr k$
Ce qui est l'équivalent à un jump à la case $k$.

### IF
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk4NjQ4MTE3Ml19
-->