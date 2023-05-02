> Source : Ulm L2 2019 https://a3nm.net/work/exams/ens/exercices_info_ulm_2019.pdf

# Chemins de Schröder 


Un chemin de Schröder de longueur $2n$ est un chemin de $(0, 0)$ à $(2n, 0)$ formés de pas unitaires nord-est et sud-est (pas $(1, 1)$ ou $(1, −1)$) ou de pas horizontaux doubles (pas $(2, 0)$), et qui de plus sont toujours au-dessus de l’axe des $x$.
Voici un exemple de chemin de Schröder :
![Chemin de Schröder](https://i.postimg.cc/Jz2gcr1h/a.png)

## Question 0
Dessiner les chemins de Schröder de longueur 2 et de longueur 4.

## Question 1
Le $n$-ième nombre de Schröder $S_n$ est défini comme le nombre de chemins de Schröder de longueur $2n$. Par convention, il existe un unique chemin de Schröder de longueur $0$. Déterminer la formule de récurrence de $S_{n+1}$ en fonction de $S_0, . . . , S_n$.

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
Soit $T$ un bosquet possédant $n$ feuilles et $p$ nœuds internes. Prouver que $T possède $n + p − 1$ arêtes.

## Question 7
Construire une bijection des bosquets à $n + 1$ feuilles vers les chemins de Schröder de longueur $2n$.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MzA0MDQwMDgsLTEwOTgzNDkwNTddfQ
==
-->