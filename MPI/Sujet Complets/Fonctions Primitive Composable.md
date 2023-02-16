> Fonction, Classes, Ensembles, Codage

Sujet tombé à l'oral L3 d'INFO théorique d'Ulm en 2021
Source : https://a3nm.net/work/exams/ens/exercices_info_ulm_2021.pdf

# Fonctions Primitives Composable

On appelle fonctions de base les fonctions suivantes :
1. la fonction constante $0$, notée $Z : \N \to \N$, et définie par $Z(n) = 0$
2. la fonction successeur $S : \N \to \N$ , définie par $S(n) = n + 1$
3. les fonctions de projection $\pi_n^i : \N^n \to \N$ définies pour $0 \le i < n \in \N$ par $\pi_n^i(x_0, . . . , x_{n−1}) = x_i$

On pose $\mathcal{C}_0$ la classe des fonctions de base.

Pour tout $f:\N^n\to \N\in\mathcal{C}_s$ et $g_1,...,g_n : \N^k \to\N \in \mathcal{C}_s$, on a $h = f\circ (g_1,...,g_n) \in\mathcal{C}_{s+1}$ définie par, pour tout $x_1,...,x_k\in\N$ : 
$$h(x_1, . . . , x_k) = f(g_1(x_1, . . . , x_k), . . . , g_n(x_1, . . . , x_k))$$

 appartient à $\mathcal{C}_{s+1}$.
 
 Soit $\mathcal{C}^∞ = \bigcup_{s=0}^\infin \mathcal{C}_s$ la plus petite classe de fonctions contenant les fonctions de base, et close par l’opération de composition définie ci-dessus.

## Question 1
Montrer que pour toute fonction $f:\N^2\to\N$ dans $\mathcal{C}_s$, la fonction $g:\N^2\to\N$ définie par 
$$
g(x,y) = f(y,x)
$$
est dans $\mathcal{C}_{s+1}$

## Question 2
Montrez qu'elle est aussi dans $\mathcal{C}_{s}$

## Question 3
Montrer que pour toute fonction $f\in\mathcal{C}_s$ de type $\N^n\to\N$, il existe un entier $0\le i \le n$ et une fonction $g\in\mathcal{C}_s$ de type $\N\to\N$ telle que pour tout $x_0,...,x_{n-1}$, on a
$$
f(x_0,...,x_{n-1}) = g(x_i)
$$
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAwNTcxMzgzMywxMjgzNDc4NTUyLC0xMz
g2ODgzMzgxLC0zMTg1NjAyNTksMTIyMDU4MzMzOSwtMzU5NTEy
ODA5XX0=
-->