
## Arbre binaire parfaits
> *INFO-1 2023 MINES MPI*

On ce donne le type d'un arbre suivant :
```c
typedef struct Noeud *arb;
struct Noeud {
  int valeur;
  arb fils_g;
  arb fils_d;
};
```

On définie un arbre binaire **parfait** tel que toute les feuilles sont à la même distance de la racine.
On dit que la hauteur de l'arbre nul (sans nœud) est -1.
1. Donnez une définition équivalente de ce type en OCaml. Toujours en OCaml, donnez la fonction `val hauteur : arbre -> int` donnant pour un arbre quelconque sa hauteur.
2. Dessinez un arbre parfait à 7 nœuds. Tout les arbres complets sont-ils parfaits ?
3. Démontrez que tout arbre parfait de hauteur $h$ possède $2^{h+1}-1$ nœuds.
4. Donnez `bool est_parfait(arb a)` renvoyant vrai si l'arbre `a` est parfait.
5. Donnez `arb arb_trouve(arb a, int k)` renvoyant le `k`ème élément dans l'ordre préfixe de l'arbre. On suppose ici que `a` est parfait et que $0\le k<n$ avec $n$ le nombre de sommets.
6. Discutez de la complexité de `arb_trouve` et de potentiel moyens de l'améliorer.

## Arbre d'ensembles de séries
On ce donne le type suivant d'arbre en Ocaml :
```ocaml
type arb = F | N of (int * arb) list;;
```

On dit que une liste d'entiers $(q_n)_{n\le p}$ appartient à un `arb` si il existe un chemin de la racine à une feuille étiqueté par $q_0,...,q_p$
1. 
1. Dessinez l'arbre représentant $\{ [ \! [0,1,0]\!]; [ \! [0,1,1]\!]; [ \! [1]\!]; [ \! [1,2]\!]\}$.
2. Montrez que si $(x_1,...,x_n,a_1,...,a_q)$ et $(x_1,...,x_n,b_1,...,b_p)$ appartiennent au même arbre 

## Tas de Fibonacci

1. Donnez en C
N. En déduire un algorithme de tri de liste en $O(n\ln n)$

## Arbres d'intervalles
Un arbre d'intervalles est un arbre binaire dont toute les feuilles contiennent un intervalle de la forme $[\![ a; b]\!]$

On ce donne le type suivant en ocaml :
```ocaml
type arbre = F of float * float | N of float * float * arbre * arbre;;
```

1. Qu'est-ce qu'un arbre binaire de recherche ? Donnez en 
2. Proposez une structure en C et en ocaml pour un arbre binaire d'intervalle.
## Arbre canonique
> *INFO A 2023 X-ENS MPI*

On définie une structure d'arbre :
```ocaml
type tree = F of int | N of tree * tree;;
``` 
Un arbre _t_ est dit *canonique* si pour $A$ et $B$ deux feuilles, on a $A$ plus proche de la racine que $B$ ssi $A$ arrive avant $B$ dans un parcours préfixe.

Un arbre canonique peut-être uniquement représenté par un tableau qui à chaque hauteur associe son nombre de sommets.

1. Donnez une définition équivalent de ce type en C. Toujours en C, donnez la fonction `void parcours(arbre* arb)` qui affiche le parcours préfixe de `arb`.
2. Donnez les arbres canonique des tableaux $[\![0;2]\!]$, $[\![0;0;3;2]\!]$, $[\![0;1;1;1;1;2]\!]$.
3. Démontrez que le tableau d'un arbre canonique non trivial doit se terminer avec un nombre pair.
4. Donnez une fonction `val canonical : int array -> tree` qui à un tableau associe son arbre canonique. On mettra sur chaque feuille son indice d'apparition dans le parcours préfixe. 


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE3MTQxMjk4NiwxNzEyMTYwMTcsLTk4MD
gxMTM5OCwxMTUyNjc1MDAsLTE5Njc3MTg3NjAsMTIxODc4NDA0
LC0zNTM4MjQ3OTIsLTMwOTE0NDEwNl19
-->