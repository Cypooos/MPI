> Sujet tombé à l'oral L4 d'INFO théorique d'Ulm en 2021

Source : https://a3nm.net/work/exams/ens/exercices_info_ulm_2021.pdf
## Fonctions Primitives Composable


On appelle fonctions de base les fonctions suivantes :
1. la fonction constante $0$, notée $Z : \N \to \N$, et définie par $Z(n) = 0$
2. la fonction successeur $S : \N \to \N$ , définie par $S(n) = n + 1$
3. les fonctions de projection $\pi_n^i : \N^n \to \N$ définies pour $0 \le i < n \in \N$ par $\pi_n^i(x_0, . . . , x_{n−1}) = x_i$

Soit $\mathcal{C}_0$ la classe des fonctions de base, et étant donné $\mathcal{C}_s$, soit $\mathcal{C}_{s+1}$ la classe qui contient les fonctions de $\mathcal{C}_s$, et telle que pour tous $n, k \in \N$, pour toutes fonctions $g_0, . . . , g_{n−1} \in \mathcal{C}_s$ de type $\N^k → \N$ et toute fonction $f \in C_s$ de type $\N^n \to \N$, la fonction $h : \N^k \to \N$ définie par
$$h(x_0, . . . , x_{k−1}) = f(g_0(x_0, . . . , x_{k−1}), . . . , g_{n−1}(x_0, . . . , x_{k−1}))$$
 appartient à $\mathcal{C}_{s+1}$.
 Soit $\mathcal{C}^∞ = \bigcup_{s=0}^\infin \mathcal{C}_s$ la plus petite classe de fonctions contenant les fonctions de base, et close par l’opération de composition définie ci-dessus.
TODO : recopier la suite...
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NDQxNjAzMV19
-->