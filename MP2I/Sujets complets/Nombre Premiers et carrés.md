>Source : Sujet Ulm 2019 J3 https://a3nm.net/work/exams/ens/exercices_info_ulm_2019.pdf

# Nombre Premiers et carrés

On dit qu’un entier naturel est sans carré s’il n’est pas divisible par le carré d’un entier supérieur ou égal à $2$.
## Question 0
Donner le pseudo-code d’un algorithme permettant de calculer le nombre d’entiers naturels sans carré inférieurs ou égaux à $n$. Quelles sont ses complexités en temps et en espace ?

## Question 1
 
On note $π(n)$ le nombre de nombres premiers inférieurs ou égaux à $n$.
On admet le théorème des nombres premiers : quand $n$ tend vers l’infini, $π(n) \sim \frac{n}{\ln n}$
Ceci implique en particulier que la valeur du $k$-ème nombre premier $p_k$ est équivalente à $k \ln k$.

Donner le pseudo-code d’un algorithme permettant de calculer $π(n)$. Quelles sont ses complexités en temps et en espace ?
## Question 2
Décrire une structure de données permettant de représenter un sous-ensemble $E$ de $[\![1, n]\!]$ et supportant les opérations suivantes :
— initialisation à $[\![1, n]\!]$ en temps $O(n)$,
— suppression d’un élément en temps $O(1)$,
— énumération dans l’ordre croissant de tous les éléments de l’ensemble $E \sub [\![1, n]\!]$ en temps $O(|E|)$.
La structure de données occupera un espace $O(n)$.

## Question 3
En déduire le pseudo-code d’un algorithme qui permet de résoudre la question 1 en temps $O(n)$.
## Question 4
Donner le pseudo-code d’un algorithme permettant de calculer tous les $p \land q$ (pgcd) pour $p, q \in [\![1, n]\!]$. Quelle est sa complexité en temps ?

## Question 5
On admet qu’il est possible d’implémenter une structure de donnée de dictionnaire dont les clés sont des entiers (non nécessairement contigus) de telle façon que tous les accès soient en temps $O(1)$.
Autrement dit, on peut se donner une structure $T$ de sorte que, pour tout entier $i \in \N$, on puisse lire la valeur T[i] ou écrire la valeur T[i] en temps $O(1)$; la structure utilise un espace mémoire $O(n)$ où $n$ est le nombre d’entiers $i$ différents pour lesquels on a écrit T[i].

On note $\Phi(n)$ le nombre de paires d’entiers $(p, q)$, avec $1 \le p \le n$, $1 \le q \le n$, et $p$ et $q$ premiers entre eux.
Démontrer la formule de récurrence :
$$
\Phi(n) = n^2+\sum_{d=2}^n \Phi(n)
$$
En déduire le pseudo-code d’un algorithme permettant de calculer $\Phi(n)$ en temps sous-linéaire par rapport à $n$. Quelles sont ses complexités en temps et en espace ?

<!--stackedit_data:
eyJoaXN0b3J5IjpbNTAwMjg4NTUwLC0xNTEwODg4NjM1LDEzMz
E1MDc4MDVdfQ==
-->