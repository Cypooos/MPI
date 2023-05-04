
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

On définie un arbre parfait tel que toute les feuilles sont à la même distance de la racine.
On dit que la hauteur de l'arbre nul (sans nœud) est -1.
1. Dessinez un arbre parfait à 7 nœuds. Tout les arbres complets sont-ils parfaits ?
2. Démontrez que tout arbre parfait de hauteur $h$ possède $2^{h+1}-1$ nœuds.
3. Donnez `bool est_parfait(arb a)` renvoyant vrai si l'arbre `a` est parfait.
4. Donnez `arb arb_trouve(arb a, int k)` renvoyant le `k`ème élément dans l'ordre préfixe de l'arbre. On suppose ici que `a` est parfait et que `k`$<2^{h+1}-1$ avec $h$ la hauteur de l'arbre.

## Arbre d'ensembles de séries
On ce donne le type suivant d'arbre en Ocaml :
```ocaml
type arb = F | N of (int * arb) list;;
```

On dit que une liste d'entiers $(q_n)_{n\le p}$ appartient à un `arb` si il existe un chemin de la racine à une feuille étiqueté par $q_0,...,q_p$
1. Dessinez l'arbre représentant $\{ [ \! [0,1,0]\!]; [ \! [0,1,1]\!]; [ \! [1]\!]; [ \! [1,2]\!]\}$, puis donnez en une définition ocaml.
2. Montrez que si $(x_1,...,x_n,a_1,...,a_q)$ et $(x_1,...,x_n,b_1,...,b_p)$ appartiennent au même arbre 

## Tas de Fibonacci


N. En déduire un algorithme de tri de liste en $O(n\ln n)$

## Arbres d'intervalles
Un arbre d'intervalles est un arbre binaire dont toute les feuilles contiennent un intervalle de la forme $[\![ a; b]\!]$

On ce donne le type suivant 

1. Qu'est-ce qu'un arbre binaire de recherche ?
2. Proposez une structure en C et en ocaml pour un arbre binaire d'intervalle.
## Arbre canonique
> *INFO A 2023 X-ENS MPI*

On définie une structure d'arbre :
```ocaml
type tree = F of int | N of tree * tree;;
``` 
Un arbre _t_ est dit *canonique* si pour $A$ et $B$ deux feuilles, on a $A$ plus proche de la racine que $B$ ssi $A$ arrive avant $B$ dans un parcours préfixe.

Un arbre canonique peut-être uniquement représenté par un tableau qui à chaque hauteur associe son nombre de sommets.
1. Qu'est-ce qu'un parcours préfixe ? Donnez `val parcours : tree -> int list` qui retourne le parcours préfixe d'un arbre. Dans notre cas, pourquoi est-il le même qu'un parcours postfixe ?
2. Donnez les arbres canonique des tableaux $[\![0;2]\!]$, $[\![0;0;3;2]\!]$, $[\![0;1;1;1;1;2]\!]$.
3. Démontrez que le tableau d'un arbre canonique non trivial doit se terminer avec un nombre pair.
4. Donnez une fonction `val canonical : int array -> tree` qui à un tableau associe son arbre canonique. On mettra sur chaque feuille son indice d'apparition dans le parcours préfixe. 


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MTk5MTg1ODgsMTIxODc4NDA0LC0zNT
M4MjQ3OTIsLTMwOTE0NDEwNl19
-->