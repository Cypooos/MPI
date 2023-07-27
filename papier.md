
# La machine de Cythan

La machine de Cythan constite en un tableau infini d'entier positifs $T[n]$ indexé par des entiers positifs.
A chaque itération de la machine, les deux opérations suivantes sont réalisées :
1. $T[0] \larr T[0]+2$
2. $T[T[T[0]-2]] \larr T[T[T[0]-1]]$

Si l'état de la machine ne change pas après une itération, alors elle s’arrête.
Pour comprendre ces deux opérations, il faut voir $T[0]$ comme l'*instruction pointer* de la machine, incrémenté à chaque itération, et voir la deuxième comme l'opération `mov T[T[0]-2] [T[T[0]-1]]` .

En fait, ces deux opérations sont équivalentes aux instructions :
1. $(v_1,v_2) = (T[IP],T[IP+1])$ avec $IP = T[0]$, l'*Instruction pointeur*
2. $T[v_1] \larr T[v_2]$
3. Si $T[0]$ n'a pas été modifié, alors $T[0] \larr T[0] + 2$

L'état initial est une suite quelconque d'entiers potentiellement infinie.

### JUMP

On considère le code 
| position |  0  | ... | $p$ | $p+1$ | $p+2$ |
|----------|-----|-----|-----|-------|-------|
| **code** | $p$ | ... |  0  | $p+2$ | $k$ |

Si l'on effectue une itération, l'on fera $T[T[T[0]+2-2]] = T[T[p]]=T[0] \larr T[T[T[0]+2-1]] = T[T[p+1]]=T[p+2]=k$, soit l'opération $T[0] \larr k$
Ce qui est l'équivalent à un `jump` à la case $k$.

### IF BOOL

On considère le code 
| position |  0  | ... | $p$ | $p+1$ | $p+2$ | $p+3$ | $p+4$ | $p+5$ | $p+6$ | $p+7$ |
|----------|-----|-----|-----|-------|-------|-------|-------|-------|-------|-------|
| **code** | $p$ | ... |  1  | $p+6$ |  $0$  |  BOOL |  $0$  | $p+7$ |  $k_\top$  |  $k_\bot$  |

Ici, si BOOL = 1, alors après 2 itérations, on aura $T[0]=k_\top$
si BOOL = 0, alors après 3 itérations, on aura $T[0]=k_\bot$
On a donc fait un saut conditionnel. 
D'une manière analogue, l'on peut faire des SWITCH, on l'on a une série de pointeurs vers lesquels sauter selon les différentes valeurs que peut prendre une case. Attention, le SWITCH ne marche que pour un nombre fini de cas, et écrasera les valeurs $T[i]$ pour tout les $i$ dans les valeurs possibles.

## Turing complete
On montre que la machine de cythan est turing complete en simulant l'automate cellulaire Rule 110, qui est Turing complete.

Pour cela, on découpe le tableau en une série de blocs $b_i$ dont on donne le code d'un $b_i$ ci-dessous.
Comme Rule 110 progresse des deux cotés, on a que le bloc $b_{2i}$ représente la case $i$ de Rule 110 et le bloc $b_{2i+1}$ représente la case $-(i+1)$

Si $i$ pair :
```
entry_i: 
  SERIE_DE_IF
	IF is_explored THEN
		JUMP entry_{i+1}
	ELSE 
		JUMP set_explored
set_explored: 
  is_explored <- one
  JUMP block_{0}
is_explored: 0
one:1
value: 0
```

Si $i$ impair :
```
entry_i: 
  SERIE_DE_IF
  JUMP entry_{i+1}
value: 0
```

Avec `SERIE_DE_IF` l'arbre de diagrame de décision permettant de mettre à jour `VALUE`$_{i}$ depuis `VALUE`$_{i-2}$, `VALUE`$_{i}$ et `VALUE`$_{i+2}$

Il y a aussi les cas $i\in\{0;1\}$ à traiter différemment (car $i-2<0$):
$b_0$ accède à $b_{1}$ et $b_2$ 
$b_{1}$ accède à $b_0$ et $b_{3}$

## Généralisation

les programmes généeré par la grammaire 
$$
S \to |\ \text{if } V\text{ then } S \text{ else } S \text{ endif}
$$
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYxMDI4NDg3LDEzNzcyMzAzMDQsMTM5NT
EyMjE4NCw4MjU3NTU3NTUsMTIwMzMzNTk4MiwtOTg2NDgxMTcy
XX0=
-->