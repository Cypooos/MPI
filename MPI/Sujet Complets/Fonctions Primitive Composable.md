> Fonction, Classes, Ensembles, Codage

Sujet tombé à l'oral L3 d'INFO théorique d'Ulm en 2021
Source : https://a3nm.net/work/exams/ens/exercices_info_ulm_2021.pdf

# Fonctions Primitives Composable


On appelle fonctions de base les fonctions suivantes :
1. la fonction constante $0$, notée $Z : \N \to \N$, et définie par $Z(n) = 0$
2. la fonction successeur $S : \N \to \N$ , définie par $S(n) = n + 1$
3. les fonctions de projection $\pi_n^i : \N^n \to \N$ définies pour $0 \le i < n \in \N$ par $\pi_n^i(x_0, . . . , x_{n−1}) = x_i$

On pose $\mathcal{C}_0$ la classe des fonctions de base.

Pour tout $g_1,...,g_n : \N^k \to\N \in \mathcal{C}_s$ et pour tout $g$

Etant donné $\mathcal{C}_s$, soit $\mathcal{C}_{s+1}$ la classe qui contient les fonctions de $\mathcal{C}_s$, et telle que pour tous $n, k \in \N$, pour toutes fonctions $g_0, . . . , g_{n−1} \in \mathcal{C}_s$ de type $\N^k → \N$ et toute fonction $f \in C_s$ de type $\N^n \to \N$, la fonction $h : \N^k \to \N$ définie par
$$h(x_0, . . . , x_{k−1}) = f(g_0(x_0, . . . , x_{k−1}), . . . , g_{n−1}(x_0, . . . , x_{k−1}))$$

 appartient à $\mathcal{C}_{s+1}$.
 
 On dira que $h$ est la composé de $f$ par $g_0,...,g_{n-1}$, on notera $h = f\circ (g_0,...,g_{n-1})$
 
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
eyJoaXN0b3J5IjpbLTE4MTE2NTM2OTUsMTI4MzQ3ODU1MiwtMT
M4Njg4MzM4MSwtMzE4NTYwMjU5LDEyMjA1ODMzMzksLTM1OTUx
MjgwOV19
-->