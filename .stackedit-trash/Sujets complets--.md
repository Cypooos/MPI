# Ulm J3 2019
> Math, arithmétique, programmation, pseudo-code et structure de données

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
On admet qu’il est possible d’implémenter une structure de donnée de dictionnaire dont les clés sont des entiers (non nécessairement contigus) de telle façon que tous les accès soient en temps $O(1)$. Autrement
dit, on peut se donner une structure $T$ de sorte que, pour tout entier $i \in \N$, on puisse lire la valeur T[i] ou écrire la valeur T[i] en temps $O(1)$; la structure utilise un espace mémoire $O(n)$ où $n$ est le nombre d’entiers $i$ différents pour lesquels on a écrit T[i].

On note $\Phi(n)$ le nombre de paires d’entiers $(p, q)$, avec $1 \le p \le n$, $1 \le q \le n$, et $p$ et $q$ premiers entre eux.
Démontrer la formule de récurrence :
$$
\Phi(n) = n^2+\sum_{d=2}^n \Phi(n)
$$
En déduire le pseudo-code d’un algorithme permettant de calculer $\Phi(n)$ en temps sous-linéaire par rapport à $n$. Quelles sont ses complexités en temps et en espace ?

# Ulm L2 2019
> Tableaux, Récurrence, Arbre 

Un chemin de Schröder de longueur $2n$ est un chemin de $(0, 0)$ à $(2n, 0)$ formés de pas unitaires nord-est et sud-est (pas $(1, 1)$ ou $(1, −1)$) ou de pas horizontaux doubles (pas $(2, 0)$), et qui de plus sont toujours au-dessus de l’axe des $x$.
Voici un exemple de chemin de Schröder :
![Chemin de Schröder](https://i.postimg.cc/Jz2gcr1h/a.png)

## Question 0
Dessiner les chemins de Schröder de longueur 2 et de longueur 4.

## Question 1
Le $n$-ième nombre de Schröder $S_n$ est défini comme le nombre de chemins de Schröder de longueur $2n$. Par convention, il existe un unique chemin de Schröder de longueur 0. Déterminer la formule de récurrence de $S_{n+1}$ en fonction de $S_0, . . . , S_n$.

## Question 2
Écrire un algorithme qui prend en entrée une liste de coordonnées $(x, y)$ triée par abscisses, et détermine s’il existe un chemin de Schröder passant par tous ces points. On considère qu’un pas horizontal passe également par son centre.
Quelle est la complexité en temps ? en mémoire ?

## Question 3
Un chemin de Schröder est aérien s’il ne comporte aucun pas horizontal au niveau du sol. Sinon, le chemin est terrestre. Soit $A_n$ le nombre de chemins aériens de Schröder de longueur $2n$.

Construire une bijection entre les chemins de Schröder terrestres de longueur $2n$ et les chemins de Schröder aériens de longueur $2n$. Que peut-on en déduire du lien entre $S_n$ et $A_n$ ?

## Question 4
Un arbre est planaire si l’ensemble des enfants d’un nœud est ordonné. Ainsi, deux arbres pouvant être rendus identiques en changeant l’ordre des enfants d’un nœud sont considérés comme différents. Un bosquet est un arbre planaire à branchement quelconque, possédant une racine, et au moins une arête, tel que tout sommet qui n’est ni une feuille, ni la racine possède au moins deux enfants.

Dessiner les bosquets possédant 1, 2 et 3 feuilles

## Question 5
Soit $B_n$ le nombre de bosquets à $n$ feuilles. Montrer pour tout $n \ge 2$ qu’il existe $B_n/2$ bosquets dont la racine possède au moins deux enfants.

## Question 6
Soit T un bosquet possédant $n$ feuilles et $p$ nœuds internes. Prouver que T possède $n + p − 1$ arêtes.

## Question 7
Construire une bijection des bosquets à $n + 1$ feuilles vers les chemins de Schröder de longueur $2n$.

# ULM L4 2019
> Ensemble, partitions, familles

Soit $F \sub \N$ et $b ∈ \N$. On note $F + b$ l’ensemble $\{a+b : a \in F\}$ et F−b l’ensemble $\{a-b : a \in F\}$.
Un ensemble $S \sub N$ est *syndétique* s’il existe un ensemble fini $F \sub \N$ tel que $\N = \bigcup_{a\in F} S − a$ .

## Question 0
Montrer qu’un ensemble $S$ est *syndétique* si et seulement s’il existe un entier $d ∈ \N$ tel que pour tout $k ∈ \N, \{k, k + 1, . . . , k + d − 1\} ∩ S \ne \empty$. On dit aussi que S est d-syndétique.

## Question 1
Parmi les ensembles suivants, lesquels sont syndétiques ?
 - (1) L’ensemble des entiers naturels
 - (2) L’ensemble des nombres pairs
 - (3) L’ensemble des nombres premiers
 - (4) $\{3n + 5 : n ∈ N\}$
## Question 2
Un ensemble $T \subseteq\N$ est épais si pour tout ensemble fini $F \subseteq \N$, il existe un $n \in \N$ tel que $F + n \subseteq T$.

Montrer qu’un ensemble T est épais si et seulement si pour tout k ∈ N, il existe un $n \in \N$ tel que $\{n, n + 1, n + 2, . . . , n + k − 1\} \subseteq T$.

## Question 3
Parmi les ensembles suivants, lesquels sont épais ?
(1) L’ensemble des entiers naturels
(2) L’ensemble des nombres pairs
(3) L’ensemble des nombres premiers
(4) $\{2^n + m : n \in \N, m ∈ \{0, . . . , n\}\}$

## Question 4
Pour toute 2-partition $A_0 \sqcup A_1 = \N$, existe-t-il toujours une partie épaisse ? syndétique ?

## Question 5
Un ensemble $S \subseteq \N$ est syndétique par parties s’il est l’intersection d’un ensemble syndétique $U$ et d’un ensemble épais $T$. Si $U$ est $d$-syndétique, alors $S$ est dit $d$-syndétique par parties.

Montrer que pour toute 2-partition $A_0 \sqcup A_1 = \N$, l’un au moins de $A_0$ et $A_1$ est syndétique par parties.

## Question 6
Soit $d ∈ \N$. Un ensemble fini $F = \{n_0 < n_1 < · · · < n_{k−1}\}$ est localement $d$-syndétique si pour tout $0 \le i < k − 1$, on a $n_{i+1} − n_i < d$.

Écrire le pseudocode d’un algorithme qui prend en entrée un ensemble fini $S$ et un entier $d \in \N$, et détermine si $S$ est localement $d$-syndétique. L’ensemble $S$ est donné comme un tableau T de
booléens où T[i] indique si i appartient à $S$. Discuter de sa complexité en temps et en espace.

## Question 7
Soit $d \in \N$. Montrer que si un ensemble S est $d$-syndétique par parties alors pour tout $k \in \N$, il existe un ensemble localement d-syndétique F de cardinalité k tel que $F \subseteq S$.

## Question 8
Soit $d \in \N$ et $S \subseteq \N$. Montrer que, si pour tout $k \in \N$, il existe un ensemble localement d-syndétique $F$ de cardinalité k tel que $F \subseteq S$, alors $S$ est d-syndétique par parties. Commenter.

## Question 9
Soit une famille $\mathscr{S}$ d’ensembles d’entiers naturels close par le haut (si $S \in \mathscr{S}$ et $T \subseteq S$, alors $T \in \mathscr{S}$ ).
La famille duale de $\mathscr{S}$ est la famille $\mathscr{T} = \{T \subseteq \N : \forall S ∈ \mathscr{S} [S ∩ T \not= ∅]\}$.

Montrer que la famille des ensembles épais est la famille duale des ensembles syndétiques.
## Question 10
Soit une famille $\mathscr{S}$ d’ensembles d’entiers naturels close par le haut. Soit $\mathscr{T}$ sa famille duale, et soit $\mathscr{A} = \{S ∩ T : S \in \mathscr{S} , T ∈ \mathscr{T} \}$ la famille intersection.

Montrer que si $A \in \mathscr{A}$ , et $X_0 \sqcup X_1 = A$, alors soit $X_0 ∈ \mathscr{A}$ , soit $X_1 \in \mathscr{A}$ .

## Question 11
En déduire que pour toute k-partition $A_0 \sqcup ... \sqcup A_{k−1} = \N$, l’un au moins des $A_0, . . . , A_{k−1}$ est syndétique par parties.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NDI4OTI4NjBdfQ==
-->