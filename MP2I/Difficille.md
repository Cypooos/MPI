L'étoile devant un exos indique que c'est une version retravaillé
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
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzA1OTA4NTkwLC0xNDIxNzE5NjIwLC0xNT
A5MTMwNzQ4LDEzNjQ3MjUxODEsNzAwNDQwNDEzLDE0NjUzNDIz
MzMsLTg2NzkxMzA2NF19
-->