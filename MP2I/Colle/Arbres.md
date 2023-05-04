
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

## Arbres d'intervalles
> Source : https://info-llg.fr/option-mp/pdf/TP_intervalles.pdf

Un arbre d'intervalles est un arbre binaire de recherche dont tous les nœuds contiennent un intervalle de la forme $[\![ a; b]\!]$, dont les clefs sont $(a,b)$ dans l'ordre alphabétique.

On ce donne le type suivant en ocaml :
```ocaml
type intervalle = int * int;;
type arbre_int = F | N of intervalle * arbre_int * arbre_int;;
```

1. Qu'est-ce qu'un arbre binaire de recherche ? Proposez une structure en C similaire à celle proposé pour représenter un arbre d'intervalles.
2. Donnez en C la fonction `int hauteur(arbre* a)` donnant la hauteur d'un arbre d'intervalle.
3. Dessinez puis donnez en OCaml arbre équilibré contenant les intervalles $\{[0;2]; [0;1]; [1;3]; [4;5]; [3;5]; [3;3]\}$
4. Donnez `val trouver : arbre_int -> intervalle -> intervalle` tel que `trouver a i`  retourne un intervalle de l'arbre `a` intersectant `i` en $O(h)$ avec $h$ la hauteur de `a`.
5. Définissez les opérations de rotations sur les arbres binaire de recherche. Donnez la fonction `val rotg : arbre_int -> arbre_int` effectuant l'opération de rotation gauche. 

On supposera écrite la fonction `val rotd : arbre_int -> arbre_int` qui effectue l'opération de rotation droite.

6. Donnez `val ajouter : arbre_int -> intervalle -> arbre_int` tel que `ajouter a i` ajoute à un arbre équilibré `a` l'intervalle `i`. On veillera à ce que `a` reste équilibré.
## Arbre canonique
> *INFO A 2023 X-ENS MPI*

On définie une structure d'arbre :
```ocaml
type tree = F of int | N of tree * tree;;
``` 
Un arbre _t_ est dit *canonique* si pour $A$ et $B$ deux feuilles, on a $A$ plus proche de la racine que $B$ ssi $A$ arrive avant $B$ dans un parcours préfixe.

Un arbre canonique peut-être représenté par un tableau qui à chaque hauteur associe son nombre de feuilles.

1. Donnez une définition équivalent de ce type en C. Toujours en C, donnez la fonction `void parcours(arbre* arb)` qui affiche le parcours préfixe de `arb`.
2. Donnez les arbres canonique des tableaux $[\![0;2]\!]$, $[\![0;0;3;2]\!]$, $[\![0;1;1;1;1;2]\!]$.
3. Démontrez que le tableau d'un arbre canonique non trivial doit se terminer avec un nombre pair.
4. Donnez une fonction OCaml `val to_array : tree -> int array` qui à un arbre canonique associe sa liste d'entiers le représentant.
5. Donnez une fonction OCaml `val canonical : int array -> tree` qui à un tableau associe son arbre canonique. On mettra sur chaque feuille son indice d'apparition dans le parcours préfixe. 


## Arbre d'ensembles de mots
On ce donne le type suivant d'arbre en Ocaml :
```ocaml
type arbre_mots = F | N of (int * arb) list;;
```
On modélise une lettre par un entier positif entre $0$ et $255$.
On dit qu'un mot $(q_n)_{n\le p}$ appartient à un `arb` si il existe un chemin de la racine à une feuille étiqueté par les lettres $q_0,...,q_p$

1. Donnez en C une structure représentant le type `arbre_mots`. Donnez `bool is_in(arbre* a, `
1. Dessinez l'arbre représentant $\{ [ \! [0,1,0]\!]; [ \! [0,1,1]\!]; [ \! [1]\!]; [ \! [1,2]\!]\}$.
2. Montrez que si deux mots sont dans le même sous-arbre qui est à une distance $n$ de la racine, alors leur $n$ premières lettres sont les mêmes.

## Tas de Fibonacci

1. Donnez en C
N. En déduire un algorithme de tri de liste en $O(n\ln n)$

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI4NTM2MzE3NSwtNzMxMDMzMTIsODY5MT
A2OTU3LC0xNDkxNDY5NjUzLDI5MzAyOTMsMjA5NTgwNTI4OCwt
MTAwMDc3Nzc3NSwxMTcxNDEyOTg2LDE3MTIxNjAxNywtOTgwOD
ExMzk4LDExNTI2NzUwMCwtMTk2NzcxODc2MCwxMjE4Nzg0MDQs
LTM1MzgyNDc5MiwtMzA5MTQ0MTA2XX0=
-->