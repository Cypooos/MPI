MP2I distance cours
# Y Combinator in Python

```py
def Y(f):
    (lambda x: f(x(x)))(lambda x: f(x(x)))

Y(Y)
```
https://fr.wikipedia.org/wiki/Algorithme_de_Kos in withad:ad)

## T-003*** Fonctions Primitives Composable
> Oraux L4 - Ulm 2021

On appelle fonctions de base les fonctions suivantes :
1. la fonction constante $0$, notée $Z : \N \to \N$, et définie par $Z(n) = 0$
2. la fonction successeur $S : \N \to \N$ , définie par $S(n) = n + 1$
3. les fonctions de projection $\pi_n^i : \N^n \to \N$ définies pour $0 \le i < n \in \N$ par $\pi_n^i(x_0, . . . , x_{n−1}) = x_i$

Soit $\mathcal{C}_0$ la classe des fonctions de base, et étant donné $\mathcal{C}_s$, soit $\mathcal{C}_{s+1}$ la classe qui contient les fonctions de $\mathcal{C}_s$, et telle que pour tous $n, k \in \N$, pour toutes fonctions $g_0, . . . , g_{n−1} \in \mathcal{C}_s$ de type $\N^k → \N$ et toute fonction $f \in C_s$ de type $\N^n \to \N$, la fonction $h : \N^k \to \N$ définie par
$$h(x_0, . . . , x_{k−1}) = f(g_0(x_0, . . . , x_{k−1}), . . . , g_{n−1}(x_0, . . . , x_{k−1}))$$
 appartient à $\mathcal{C}_{s+1}$.
 Soit $\mathcal{C}^∞ = \bigcup_{s=0}^\infin \mathcal{C}_s$ la plus petite classe de fonctions contenant les fonctions de base, et close par l’opération de composition définie ci-dessus.
## M-005*
On fixe un tableau d'entier global $T$ de taille `n`
On ce donne deux fonctions `f: int -> int` et `g: int -> int`.
On cherche à calculer $T$ tel que $T[i] = g(f(i))$ ou la fonction $f$ n'est évalué que par un fil et la fonction $g$ par un autre.
Proposer une méthode avec des mutex et sémaphore. 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkxNzI0NDA2MywxMTAyOTAzOTYwLC0xNj
IxNzE5NTY3LDE1MDcxMjA2MDQsNzMwOTk4MTE2XX0=
-->