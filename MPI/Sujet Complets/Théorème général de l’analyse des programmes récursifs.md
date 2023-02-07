> Fonction, Récursivité, Équivalents, Analyse de programme

Sujet P1 d'INFO théorique d'Ulm en 2021
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
Donner les valeurs de $a, b$ et une estimation asymptotique de $f(n)$ sous la forme d’un Θ(g(n)) pour le cas de l’algorithme de recherche par dichotomie dans un tableau de taille $n$.
## Question 1
Donner sous la forme de pseudo-code l’algorithme de tri fusion.
En déduire les valeurs de $a, b$ et une estimation asymptotique de $f(n)$ sous la forme d’un $Θ(g(n))$ pour le cas de l’algorithme de tri fusion d’une liste de $n$ éléments.

On cherche maintenant à résoudre la formule de récurrence définissant $T(n)$ dans le cas le plus  
général possible pour permettre de déterminer la complexité asymptotique de l’algorithme $\mathcal{A}$.
## Question 2
Représenter les appels récursifs effectués par $\mathcal{A}$ sur une entrée de taille $n$ sous la forme d’un arbre dont la racine représente l’appel principal et les enfants d’un nœud les appels récursifs directs effectués.
On indiquera comme étiquette d’un nœud de l’arbre la taille de l’entrée.

## Question 3
Pour un certain $k\in\N$ fixé et inférieur à la hauteur de l’arbre, combien de nœuds de  
profondeur $k$ (c’est-à-dire, à distance  k  de la racine) cet arbre comporte-t-il ?

## Question 4
Exprimer la hauteur de l’arbre en fonction de $n$ et $b$.

## Question 5
Montrer l’égalité suivante :
$$
T(n) = \Theta(n^c) + \sum_{k=0}^{\log_b(n-1)}a^kf\Big(\frac{n}{b^k}\Big)
$$
où $c = \log_b(a)$

## Question 6

Montrez que si $f(n) = O(n^{c'})$ avec $c' < c$, alors $T(n) = \Theta(n ^c)$

## Question 7

Montrez que si $f(n) = \Theta(n^c)$, alors $T(n) = \Theta(n ^c\log n)$

## Question 8

Montrez que si $n^{c'}=O(f(n))$ avec $c'>c$ et si $a\times f(\frac{n}{b}) \le \alpha f(n)$ pour un certain $\alpha\in ]0;1[$, alors $$T(n) = \Theta(f(n))$$

## Question 9
Retrouver la complexité de la recherche par dichotomie et du tri fusion avec ce théorème.

## Question 10
En utilisant ce théorème, donner la complexité d'un problème dont la complexité est décrite par la formule de récurrence suivante 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMzMTY4MjQ2MSwtNzk5Nzc3Njk1LC0xMz
YwNjk2MTE0XX0=
-->