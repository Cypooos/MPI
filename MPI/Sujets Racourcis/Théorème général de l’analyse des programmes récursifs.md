> Fonction, Récursivité, Équivalents, Analyse de programme

Sujet P1 d'INFO théorique d'Ulm en 202, retravaillé pour qu'il soit plus rapide et plus difficile
Il me semble d'une importance cruciale de par à quel point il est général
Source : https://a3nm.net/work/exams/ens/exercices_info_ulm_2021.pdf
# Théorème général de l’analyse des programmes récursifs
Étant données deux fonctions $f, g : \R^+ \to \R+$, on note $f (n) = \Theta(g(n))$ si $f(n) = O(g(n))$ et $g(n) = O(f(n))$.  
On considère dans ce problème un algorithme récursif $\mathcal{A}$ prenant une entrée de taille $n \in \N^*$. On suppose que :
 - Si $n = 1$,  $\mathcal{A}$ met un temps borné par une constante ;  
 - Pour $n > 1$, $\mathcal{A}$ fait un nombre $a\in\N^*$ d’appels récursifs à $\mathcal{A}$ sur une entrée de taille $\frac{n}{b}$ ($b$ est un  
rationnel strictement plus grand que 1), ainsi qu’un certain nombre d’autres opérations dont le temps est $f (n)$.

Ainsi, le temps $T(n)$ pris pour résoudre le problème au rang $n$ est :
$$
T(n) = a\times T\Big(\frac{n}{b}\Big) + f(n)
$$
Par simplicité, on supposera dans tout le problème qu’on applique toujours l’algorithme à un $n$ pour  
lequel $\frac{n}{b}$ est un entier, y compris lors des appels récursifs.
## Question 0
Donner les valeurs de $a, b$ et une estimation asymptotique de $f(n)$ sous la forme d’un Θ(g(n)) pour les algorithmes suivants :
1) L’algorithme de recherche par dichotomie dans un tableau de taille $n$.
2) L’algorithme de tri fusion d’une liste de $n$ éléments.
3) L'algorithme du calcul du carré d'une matrice naïf

On cherche maintenant à résoudre la formule de récurrence définissant $T(n)$ dans le cas le plus  
général possible pour permettre de déterminer la complexité asymptotique de l’algorithme $\mathcal{A}$.
## Question 1
Représenter les appels récursifs effectués par $\mathcal{A}$ sur une entrée de taille $n$ sous la forme d’un arbre dont la racine représente l’appel principal et les enfants d’un nœud les appels récursifs directs effectués.
On indiquera comme étiquette d’un nœud de l’arbre la taille de l’entrée.

Montrer l’égalité suivante :
$$
T(n) = \Theta(n^c) + \sum_{k=0}^{\log_b(n-1)}a^kf\Big(\frac{n}{b^k}\Big)
$$

où $c = \log_b(a)$

## Question 2

1) Montrez que si $f(n) = O(n^{c'})$ avec $c' < c$, alors $T(n) = \Theta(n ^c)$

2) Montrez que si $f(n) = \Theta(n^c)$, alors $T(n) = \Theta(n ^c\log n)$

3) Montrez que si $n^{c'}=O(f(n))$ avec $c'>c$ et si $a\times f(\frac{n}{b}) \le \alpha f(n)$ pour un certain $\alpha\in ]0;1[$, alors $T(n) = \Theta(f(n))$

## Question 9
Retrouver la complexité des algorithmes de la question 0.

## Question 4
Le théorème s'applique-t-il à toutes les récurrences de la forme $T(n) = a\times R(\frac{n}{b}) + f(n)$ ?

<!--stackedit_data:
eyJoaXN0b3J5IjpbODAyNzI3OTUzXX0=
-->